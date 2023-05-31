---
## Configuration:

* ### Run the functions at Docker:

If you <strong>do not</strong> have Docker Installed, follow these steps:
First, run the following in your terminal:

```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```
Then to run the container you have to follow these steps:
```
docker pull kazakos13/common-functions
docker run -p 8080:8080 -it kazakos13/common-functions
"
```
If you want to push a new container first you have to go inside the smart-city-app/subflows/common-functions folder (the parent folder of this README), then open the terminal and finally follow these steps:
```
docker build -t kazakos13/common-functions .
docker push kazakos13/common-functions:latest
```

You can find the docker repo [here](https://hub.docker.com/r/kazakos13/common-functions)