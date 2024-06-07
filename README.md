# About

This is a project about managing an Accommodation System, like Booking.com . It comprises of backend and frontend components. 

## Backend
The backend component are the servers handling the requests for the accomodations, including booking, reviewing and filtering rooms. It follows the Map Reduce framework where there's a Master node receiving the requests from the user and the manager, and delegates the requests to the Worker nodes, each of which saves a number of rooms. There's also a Reducer Node that is used to aggregate the results from the Worker nodes when filtering rooms, and send it back to the Master node.

All the servers are multithreaded to handle multiple requests at the same time, and also handle synchronization issues when accessing shared resources.

The backend system also uses active replication. This means that all the Worker nodes also save the rooms of all the other Worker nodes in a HashMap containing all the replica rooms for every other Worker node. This way when a Worker Node is down, the requests are rerouted to a Worker node that is up and running, and thus using the the replica rooms. Also for every request received by the Master node, the replica rooms are also updated.


## Frontend

As for the frontend component there's 2 cli apps and one android app.

The first cli app is the one for the Manager, who is responsible for adding the rooms to the backend system. This cli app can also show the rooms that were added by the manager and the bookings for his rooms.

The second cli app is the one for the User, who can book, review and search rooms added in the backend system.

The android app has the same functionality as the user cli app.


# How to use

## Setting up Backend system
First, you have to set up the backend component. You have to run the Master, Worker and Reducer classes. Before that you have to edit the config.properties file with the correct values for the local ip and port of the Master, Reducer and Workers. 

This project is configured to be run on the same network. To acquire the local ip of your machine you can use the following command in the command prompt:

```
ipconfig
```

The Master and Reducer nodes can be run on the same or different machines.

There's multiple ways to run the Worker nodes. One way it to run multiple Worker nodes on the same machine. To do that make sure that all Worker ports are different. Then to run each Worker node, insert a parameter to declare which Worker node to run. For example to run Worker node 2 insert 2 as the parameter.

To run the Worker nodes at different machines you dont have to insert any parameter.

In all cases make sure to update the config file in all machines running a server of the backend component.

## Using Frontend component
First you have to build the project to download the org.json dependency from the maven file.

Then you have to run the Manager class to add some rooms in the backend system. There's already some rooms in the rooms directory. You can add your own custom rooms by saving a json file in the rooms directory in the following form:

```
{
	"roomName": "Olive Retreat",
	"noOfPersons":"4",
	"area": "Athens",
	"stars": "4.1",
	"noOfReviews": "2472",
	"price": 80,
	"roomImage": "images/olive_retreat.jpg"
}
```

When you add a room you are asked to select an image from the images directory. You can add your own images by saving an image in the images directory.

After that you can either use the User cli app or the android app to search, book and review a room.

Make sure to edit the config file on the machines that you use the Manager and User cli apps. In the Android app you can edit it when first opening the app.
