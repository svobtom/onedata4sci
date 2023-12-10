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

