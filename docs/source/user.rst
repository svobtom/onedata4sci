# User documentation

## How to get data
After the samples are scanned and, in some cases, even during the acquisition user can access the files in various ways. 

### Web share - download to the local computer
After scanning the sample is complete you receive e-mail on given e-mail addresses with information how to download desired data. The message contains a link to Onedata web interface where you can browse scanned files (no login required). You can download the whole dataset or only some its parts.
 
Fig. – Web share

Provisioned instance of Onedata Oneprovider
If you would like to

### Web access through Onedata

### Mount on a local computer
Onedata provides command-line application Oneclient to access stored data mounted on local computer. Your spaces are mounted as directories in specified path. You can work with the date within this folder in a normal POSIX way (you can use commands like ls, cp, …). 
Oneclient can be install on Linux by following command. It can be run on several Linux distro (Ubuntu, Fedora, Debian, CentOS). 
curl -sS http://get.onedata.org/oneclient.sh | bash
Oneclient run by:
oneclient -t <ACCESS_TOKEN> -H <PROVIDER_IP> <MOUNT_PATH>
Further reading about Oneclient: 
https://onedata.org/#/home/documentation/stable/doc/using_onedata/oneclient.html

### Use in Infrastructure manager
-----------------------------
This chapter will describe how Scipion with a dataset can be run. 
To be done...

In this chapter are described method to access data stored in Onedata system. We describe in this documentation Onedata system managed by Onezone located at https://datahub.egi.eu, but it is applicable also on another Onezone instances. Method of sign in and propagation of groups can be different there. 

## Set up permissions in Onedata

Add user to EGI Check-in group
Go to https://aai.egi.eu and log in with identity from your institution.
Click on item Groups in the left menu and choose My Groups. You will see groups you are belong to. 
At the top right bottom there is a link Manage groups. On this page you can add user to existing groups (provided you have appropriate access right to the group) or you can create a new group.
Then You can add users to the group. You click on the group name and following on Manage group Memberships. On this page you can choose user to add to the group. User should use EGI check-in to be in the list.

Web access
If you have a link to desired data, click on the link. You can also sign in Onedata Onezone, where you can find spaces with


