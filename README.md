# Smart City App
This is a smart city app that saves many cities (and their rankings, weather and other data) according to some APIs (which can be found [here](https://docs.google.com/document/d/1qboEuLH-l-9isQfCn9RzCzkCyO4TYGtqEFc8UejJHHo/edit?usp=sharing)). 

---
## Geonames Account Configuration
To configure the username, go to the gui diagram and set it in the "GLOBAL USER CONFIG" component (replace it where it says yourusername).

---
## How to use the app
You can initialize the app GUI by pressing in the gui-dataflow the inject button (currently with name: "INITIALIZE DROPDOWN"). After injecting, go to http://localhost:1880/ui/ and select a country. All the wanted data of the available cities of the selected country should be saved inside an sqlite db in /tmp folder, called cities.db!
