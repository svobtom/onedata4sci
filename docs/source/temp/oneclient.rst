Oneclient usage
===============

# run docker container with Pepa's oneclient
docker run -it --rm --privileged --name oneclient -v /tmp:/host-tmp --entrypoint=/bin/bash jhandl/csi-onedata

# prepare access token
echo "xxx" > token.txt

# create folder which will be used as mountpoint
mkdir onedata

# mount spaces
oneclient -H ip-147-251-21-190.flt.cloud.muni.cz -t `cat token.txt` onedata