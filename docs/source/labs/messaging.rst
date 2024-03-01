Messaging
=============

``fs2od`` (filesystem to Onedata) software can interact with the user (one-way only) using Messaging features. This allows the user to stay informed about critical actions the system takes or will take, and allows the user to respond to these actions.

Actions supported
 - Creating new dataset
 - Moving dataset from primary provider to secondary providers
 - Removing old dataset

Each of the following methods can be enabled separately and will work independently.

Email
-----
This is the only communication method yet supported. The implementation complies with `RFC 821 <https://www.rfc-editor.org/rfc/rfc821>`_ (and its extensions) for Simple Mail Transfer Protocol, `RFC 822 <https://www.rfc-editor.org/rfc/rfc822>`_ for specification of the sender/receiver format and `RFC 8314 <https://www.rfc-editor.org/rfc/rfc8314>`_ for the TLS in emails.

Overview
++++++++
Using the email allows user to connect to a selected SMTP server using a selected port. This method allows variety combinations of the encryption such as ``SSL`` (not recommended), ``TLS``, ``STARTTLS`` and ``ANY``. It also allows the user to select login and password if auth is required.

This feature also allows the categorization of the email recipients; it can send the message using ``to`` (To), ``cc`` (Carbon Copy) or ``bcc`` (Blind Carbon Copy) and definitely combine this categories for the selected recipient. The recipient can be defined either as an immutable value, or as the pointer to the value stored in metadata file as well.

Credentials configuration
+++++++++++++++++++++++++
Configuration can be found under sections ``messaging->credentials->email``

- ``enabled`` - Tells the software to use (``True`` - enabled) or not to use (``False``) the email messaging system. If enabled, the software will check for the server connection availability in the pre-running setup and it will log with very high severity if the server is not available.

.. note::

    The communication server unavailability (the server is down) is not enough sufficient reason for ``fs2od`` to crash. If sending the message failed, the corresponding information is passed to the log with the highest severity and the user is thus notified.

- ``smtpPort`` - Specifies the used port. If the value is 0 or not provided at all and provided ``encryptionMethod`` is correct, it will select the default port based on this method (465 for ``SSL``/``TLS``, 587 for ``STARTTLS`` and 25 for ``ANY``)
- ``encryptionMethod`` - Allowed values are:
    -  ``SSL`` - this is not recommended due to security reasons, so this option is only an alias for TLS
    -  ``TLS`` - implicit encryption - the client connects to the server knowing that it supports TLS as default
    -  ``STARTTLS`` - explicit encryption - the client connects to the server using unencrypted connection and will negotiate with the server to upgrade to the encrypted connection
    -  ``ANY`` - this is not recommended, but some servers requires it, this is the communication-long unencrypted connection which can be eavesdropped
- ``messageSender`` - The value in the format "Name Surname <user\@mail.tld>" or the plain email address. All the emails will be send with the sender set to this value. It is important to think about this value as some spam filters block addresses such as "noreply\@mail.tld" or similar

Receiver commands
+++++++++++++++++
The ``fs2od`` utility introduces new Messaging Email Service commands. The command tells the program, how to process email strings in the scope of sending to a specific user, sending using different mode or selecting the specific user from another source.

Available commands:
 - ``to:`` - Sets the computed receiver's category (destination) to ``to`` (To). If no other category command is used, this command is noop as the default behavior is to send an email using this category
 - ``cc:`` - Sets the computed receiver's category (destination) to ``cc`` (Carbon Copy)
 - ``bcc:`` - Sets the computed receiver's category destination to ``bcc`` (Blind Carbon Copy)
 - ``metadata:`` - Changes the way of computing the message receiver. The default option (without this command) is sending the email to address specified after removing all the commands. The command changes this behaviour and the receiver is computed using the `definition metadata file <./fs2od.html#application-configuration>`_. The value should be in the format of "metadata:Where->To->find". The resulting value (the final receiver) is then computed as config["Where"]["To"]["Find"].

.. note::
    Using the Messaging Email Service record with ``metadata:`` command works as a best-effort service. If the desired value is not found, the receiver entry is omitted, and the email is not sent using the entry (it is still logged). This results in the fact that the only way to be sure that the email was sent is to provide it as absolute value (not using metadata command).

All of the commands can be combined, the order does not matter. However, the commands are idempotent and providing the same command multiple times does not cause e.g. the email to be sent more times to the same user under the same category. On the other side, using the commands as e.g. ``to:bcc:cc:`` sets the computed recipient to all of the three categories, so the email is sent three times.

.. warning::
    The commands are case sensitive. Using anything different than lower case might cause an undefined behaviour.

Service configuration
+++++++++++++++++++++
Configuration can be found under sections ``messaging->email``

- ``to`` - Separate lists of the receivers under a specific category. Yet, the two categories are used: ``space_creation`` and ``space_deletion`` for specifying the recipients of the notifications about dataset creation and dataset deletion respectively. The entry format is defined under `Receiver Commands <#receiver-commands>`_.
- ``timeBeforeAction`` - List of the internal time-defining relative timestamps which tell when the email should be sent before the specific action is taken. The time format is defined under `Internal timestamps <./archiving_expiring.html#internal-timestamps>`_. The sending action is idempotent; the email is sent only once after the timestamp passes.
- ``language`` - Case insensitive country code used for message templates representing the localization of the email contents. Built-in templates comply with `ISO 639-1 <http://xml.coverpages.org/N071-PWD-639-lang-group-coding.pdf>`_ and it is strongly recommended to continue with this identifiers. The built-in templates can be extended by user's own templates, they only need to be mounted among the others. The default (implicit) language is ``en`` (English); if none language is set or the message template is not found, the original version is used.