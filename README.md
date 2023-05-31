# Smart City App
This is a smart city app that saves many cities (and their rankings, weather and other data). Also within this repo, there are solutions for the <strong>hackathon 2023 challenges</strong>.You can view a detailed description of this project and the challenges [here](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing). You can checkout the app for yourself by installing [Node-RED](https://nodered.org/). Before you run the app, you should follow the prerequisites and configuration steps specified in the corresponding sections of this README.

---
## Prerequisites - Docker Installation:
Before you start this app, it is recommended to install a docker image that was developed for the common-functions challenge of <strong>hackathon 2023</strong>. Here are the commands to install and run this image:
```
docker pull kazakos13/common-functions
docker run -p 8080:8080 -it kazakos13/common-functions
```
If you dont want to install this docker image you should not encounter any problems in the execution of the app, because some local flows were developed, which have the same functions as the docker image (and they are executed if the docker image is not running).
<br>
You can also read the overview of the docker image [here](https://hub.docker.com/r/kazakos13/common-functions).

---
## Configuration:
The <strong>only</strong> diagram needed for import in order for the project to run is the gui_res.json (you can import it in node-red). Once you do that, please refer to the following configuration steps:

* ### Account Configuration

To configure your account settings, follow these steps:

1. Open the `GUI_RES` flow and locate the `init GUI` node.
2. Click on the node to access the configuration options.
3. In the configuration panel, you will find several required keys and usernames.
4. Provide your Geonames username by entering it in the `GEONAMES_USERNAME` input field. This is necessary for the app to function properly.
5. Additionally, you need to enter your API keys for the OpenWeatherMap, Weather API, and Tomorrow API. Insert your keys in the `OPENWEATHER_KEY`, `WEATHERAPI_KEY`, and `TOMORROW_KEY` inputs, respectively.
   - Note: If you leave these keys empty or as "yourkey", the app will not produce errors, but you may experience data loss in the GUI, particularly in the current weather section.
6. Lastly, if desired, you can configure the `MAP_URL` by changing the domain to which the map URL points.

By following these configuration steps, you can ensure that the app works correctly and displays accurate information.

* ### RabbitMQ Config:
For these dataflow diagrams, this package is installed (from manage pallete):<br>
<strong>@node-red-tools/node-red-contrib-amqp</strong>
<br>
Once you created the rabbitmq user and vhost (with correct permissions - if you dont have any user ready, see RabbitMQ Installation section) go to the GUI City Results dataflow in the amqp server node (it is called amq.direct in the dataflow) and click on the edit button of the server (which should be localhost:5672). Then, set the username and password in the Security tab with the ones you put in the commands above. Also in the Connection tab, add the vhost name you specified in the commands above.
<br>
Lastly, put the USERNAME and PASSWORD in every http request of "Create AMQP User" dataflow (in the username and password). You should also put the username in the "RABBIT & MAP CONFIG" component of the initial Ergasia - GUI diagram.

* ### RabbitMQ Installation:

If you <strong>do not</strong> have RabbitMq Installed, follow these steps:
First, run the following in your terminal:

```
sudo apt-get install rabbitmq-server
sudo rabbitmq-plugins enable rabbitmq_management
sudo rabbitmqctl add_user USERNAME PWD
sudo rabbitmqctl set_user_tags USERNAME administrator
sudo ufw allow 15672
```
Then, you should create a vhost and give permissions (replace VHOST_NAME with "testing" or any other name you want, just keep in mind that you will also need to change it in the dataflow diagram):
```
sudo rabbitmqctl add_vhost VHOST_NAME
sudo rabbitmqctl set_permissions -p VHOST_NAME USERNAME "." "." ".*"
```
Also you will need to <strong>bind</strong> a queue to the vhost in gui (go to http://localhost:15672 and login with the credentials you put earlier). To do that, go to queues section then click on your virtual host, go to bindings, "Add binding to this queue" and put amq.direct in "From exchange" label. Then click on bind.
<br>
Then to add this user to the dataflow you can follow the rest of the steps as shown in the RabbitMQ Config Section.

---
## How to run the app
The <strong>only</strong> diagram needed for import in order for the project to run is the gui_res.json (you can import it in node-red). Once you do that and you have done the configuration correctly, press deploy (in node-red) and go to http://127.0.0.1:1880/ui.
<br>There you will find the gui of the app. You should press the "Reset" button in order to initialize the dropdown list with the available countries. Once you choose a country, click on next to see its cities and their data.


---
## Other links:
* [Project documentation](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing)
* [Weather Code Website](https://www.nodc.noaa.gov/archive/arc0021/0002199/1.1/data/0-data/HTML/WMO-CODE/WMO4677.HTM)
