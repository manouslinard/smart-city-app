In this folder, you can find the subflow we have implemented for the common functions challenge. Specifically, we have developed a docker image which has three functions:
* Quicksort
* Kmeans Clustering
* Weighted Average

This docker image can also run with openwhisk ([here](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit#bookmark=id.j3wtc5rmsiuz) is a tutorial on how to send the correct input data and get the result).

---
## Openwhisk Run:

If you do not have openwhisk already installed, check the slides of this [presentation](https://github.com/gkousiouris/2ndPHYSICSHackathon/blob/main/2nd%20Hackathon.pdf), and follow the instructions.

First of all configure the whisk properly using this commands :
```shell
wsk property set --apihost https://10.100.59.208
wsk property set --auth 23bc46b1-71f6-4ed5-8c54-816aa4f8c502:123zO3xZCLrMN6v2BKK1dXYFpXlPkccOFqm12CdAsMgRU4VrNZ9lyGVCGuMDGIwP
```
Once you have pulled the docker image and run it, do the following to create the openwhisk action:
```shell
wsk action create <action_name> --docker kazakos13/common-functions
```

In the following examples, we set <action_name> to “functionstest”.

Here is a test run of the weighted average in openwhisk:
```shell
wsk -i action invoke functionstest --param data '{
  "temperature": [
    { "value": 20, "date": 1664515200000 },
    { "value": 23, "date": 1664774400000 },
    { "value": 18, "date": 1664428800000 },
    { "value": 25, "date": 1664601600000 },
    { "value": 22, "date": 1664688000000 }
  ],
  "humidity": [
    { "value": 20, "date": 1664515200000 },
    { "value": 23, "date": 1664774400000 },
    { "value": 18, "date": 1664428800000 },
    { "value": 25, "date": 1664601600000 },
    { "value": 22, "date": 1664688000000 }
  ]
}' --param reverse false --param function wavg
```
Then you take the id and run the following:
```shell
wsk activation get -i <activation_id>
```

You should take a result like so (it is in “value”[“data”]):
```shell
ok: got activation 1715ad361b08410495ad361b080104cf
{
    "namespace": "guest",
    "name": "functionstest",
    "version": "0.0.1",
    "subject": "guest",
    "activationId": "1715ad361b08410495ad361b080104cf",
    "start": 1685626783313,
    "end": 1685626783349,
    "duration": 36,
    "statusCode": 0,
    "response": {
        "status": "success",
        "statusCode": 0,
        "success": true,
        "result": {
            "action_name": "/guest/functionstest",
            "action_version": "0.0.1",
            "activation_id": "1715ad361b08410495ad361b080104cf",
            "deadline": "1685626843312",
            "namespace": "guest",
            "transaction_id": "yMRST8JTpAuVWehNNLe4Y2hP9wtIneHY",
            "value": {
                "data": {
                    "humidity": 22.4,
                    "temperature": 22.4
                },
                "function": "wavg",
                "reverse": false
            }
        }
    },
    "logs": [],
    "annotations": [
        {
            "key": "path",
            "value": "guest/functionstest"
        },
        {
            "key": "waitTime",
            "value": 435
        },
        {
            "key": "kind",
            "value": "blackbox"
        },
        {
            "key": "timeout",
            "value": false
        },
        {
            "key": "limits",
            "value": {
                "concurrency": 1,
                "logs": 10,
                "memory": 256,
                "timeout": 60000
            }
        }
    ],
    "publish": false
}
```

Here is also a input for running quicksort in openwhisk:
```shell
wsk -i action invoke functionstest --param data '{
  "temperature": [
    { "value": 20, "date": 1664515200000 },
    { "value": 23, "date": 1664774400000 },
    { "value": 18, "date": 1664428800000 },
    { "value": 25, "date": 1664601600000 },
    { "value": 22, "date": 1664688000000 }
  ],
  "humidity": [
    { "value": 20, "date": 1664515200000 },
    { "value": 23, "date": 1664774400000 },
    { "value": 18, "date": 1664428800000 },
    { "value": 25, "date": 1664601600000 },
    { "value": 22, "date": 1664688000000 }
  ]
}' --param reverse true --param function quicksort
```

Similarly, you run the following to get the result:
```shell
wsk activation get -i <activation_id>
```

To change between functions, put the desired function in the “function” param. Your options are: 
wavg
quicksort
kmeans

the input should be similar to the one specified in the docker image.

** make sure to have put the credentials key in the .node-red/settings.js before running wsk activation get -i:
```shell
module.exports = {
  // ...
  credentialSecret: 'your-credential-secret',
  // ...
};
```




---
## Docker Push and Pull Commands:

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
If you want to push a new container first you have to go inside the smart-city-app/hackathon/common_functions folder (the parent folder of this README), then open the terminal and finally follow these steps:
```
docker build -t kazakos13/common-functions .
docker push kazakos13/common-functions:latest
```

You can find the docker repo [here](https://hub.docker.com/r/kazakos13/common-functions)
