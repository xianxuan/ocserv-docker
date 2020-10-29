# ocserv-docker
## install docker
apt-get install -y\
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

apt-get update
apt-get install -y docker-ce 

## make & run

docker build --no-cache -t ocserv-docker .

docker run -d --privileged --name ocserv-docker -v ~/ocserv-docker/ocserv:/etc/ocserv -p 443:443 ocserv-docker


## add user
docker exec -it $(docker ps -a | grep vpn_run | awk '{print $1}') ocpasswd
