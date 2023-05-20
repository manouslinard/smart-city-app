# Smart City App
This is a smart city app that saves many cities (and their rankings, weather and other data) according to some APIs (which can be found [here](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing)). You can checkout the app for yourself by installing [Node-RED](https://nodered.org/).

---
## Configuration:
* ### Geonames Account Configuration
To configure the username, go to the gui diagram and set it in the "GLOBAL USER CONFIG" component (replace it where it says yourusername).

* ### Map Url:
In the first gui diagram at "CONFIG MAP URL" component you can also set the url of the worldmap in the attribute map_url. By default, this value is http://127.0.0.1:1880/worldmap/ 

* ### Link Connections:
Github repo does not save the connections (link in and outs) of this project. Once you cloned this repo, you should go to the dataflow in [node-red server](http://127.0.0.1:1880/) and connect the links according to the comments (they are right next to them). All the links should be configured correctly in order for the app to work.

* ### OpenWeatherMap API key:
You also have to set your openweathermap api key in the first gui diagram at "CONFIG MAP URL" component in the attribute open_weather_appid.

* ### RabbitMQ Installation and Config:
```
sudo apt-get install rabbitmq-server
sudo rabbitmq-plugins enable rabbitmq_management
sudo rabbitmqctl add_user USERNAME PWD
sudo rabbitmqctl set_user_tags USERNAME administrator
Open firewall for admin panel
sudo ufw allow 15672
```
<br>
For these dataflow diagrams, the username for rabbitmq is "rabbit" and the password is "pass123" (so replace USERNAME with "rabbit" and PWD with "pass123").<br>
If you want to change this user, you can create a new one by following the instructions (or use an existing one). Keep in mind that you also have to change the username and password in the Security tab of the amqp server node (it is called amq.direct in the dataflow) in the GUI City Results dataflow.


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
