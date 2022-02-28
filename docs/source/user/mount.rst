Mount on a local computer
=========================

Onedata provides command-line application Oneclient to access stored data mounted on local computer. Your spaces are mounted as directories in specified path. You can work with the date within this folder in a normal POSIX way (you can use commands like ls, cp, …). 
Oneclient can be install on Linux by following command. It can be run on several Linux distro (Ubuntu, Fedora, Debian, CentOS). 
curl -sS http://get.onedata.org/oneclient.sh | bash
Oneclient run by:
oneclient -t <ACCESS_TOKEN> -H <PROVIDER_IP> <MOUNT_PATH>
Further reading about Oneclient: 
https://onedata.org/#/home/documentation/stable/doc/using_onedata/oneclient.html

.. todo: specific instructions how to obtain the token, and provider IP/name
