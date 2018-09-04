This is a Oracle Linux image with sshd support for usage with Ansible

The base image is the one tagged latest form https://hub.docker.com/_/oraclelinux/

The Dockerfile in this repo is based on https://docs.docker.com/engine/examples/running_ssh_service/

--------
1) Build:

./build.sh
--------
2) Run:

docker run -d -p 22:22 --name test_sshd 12factormx/oraclelinux:latest
--------
3) Check you cointainer ip:

docker inspect --format '{{ .NetworkSettings.IPAddress }}' test_sshd
--------
4) Connect (password for root is root):

ssh root@\<your container ip\>
--------
5) Enjoy.

Some note on key securty:

This Dokerfile creates the key inside the container. For greater secury yo can modify this docket file to store the keys on the host and modify the /etc/ssh/sshd_conf for serching the keys on a host mounted volume. Hope to have some time to work on this soon.


