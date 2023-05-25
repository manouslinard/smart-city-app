# Smart City App
This is a smart city app that saves many cities (and their rankings, weather and other data) according to some APIs (which can be found [here](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing)). You can checkout the app for yourself by installing [Node-RED](https://nodered.org/).

---
## Configuration:
* ### Geonames Account Configuration
To configure the username, go to the gui diagram and set it in the "GLOBAL USER CONFIG" component (replace it where it says yourusername).

* ### Map Url:
In the first gui diagram (Ergasia - GUI) at "RABBIT & MAP CONFIG" component you can also set the url of the worldmap in the attribute map_url. By default, this value is http://127.0.0.1:1880/worldmap/ 

* ### Link Connections:
Github repo does not save the connections (link in and outs) of this project. Once you cloned this repo, you should go to the dataflow in [node-red server](http://127.0.0.1:1880/) and connect the links according to the comments (they are right next to them). All the links should be configured correctly in order for the app to work.

* ### OpenWeatherMap API key:
You also have to set your openweathermap api key in the first gui diagram (Ergasia - GUI) at "RABBIT & MAP CONFIG" component in the attribute open_weather_appid.

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
## How to use the app
You can initialize the app GUI by pressing in the gui-dataflow the inject button (currently with name: "INITIALIZE DROPDOWN") - if you have node-red installed and running (run node-red in terminal), you can view the dataflow diagrams at http://127.0.0.1:1880/
<br>
By initializing the dropdown this way, you also create the db and set the correct global variables (it is recommended if you want to restart the app). 
<br>
After injecting, go to http://127.0.0.1:1880/ui/ and select a country. All the wanted data of the available cities of the selected country should be saved inside an sqlite db in /tmp folder, called cities.db!


---
## Other links:
* [Project documentation](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing)
* [Weather Code Website](https://www.nodc.noaa.gov/archive/arc0021/0002199/1.1/data/0-data/HTML/WMO-CODE/WMO4677.HTM)
