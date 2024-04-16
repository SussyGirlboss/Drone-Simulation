# Drone-Simulation

Authors: Rock Zgutowicz, Derrick Dischinger, Minh Tong, Leni Roeser

Docker container: 
https://hub.docker.com/repository/docker/sussygirlboss/team-010-43-hw4-extension/general

This project is about using the principle rules of software design to add features to an existing codebase while maintaining a modular system. The codebase, before we began, allowed a user to schedule packages to be delivered to robots via drone. Through the interface, the location of the package and the robot can be chosen, as well as the pathing strategy for the drone to use on the way to the robot once it picks up the package.

The simulation runs primarily in the SimulationModel class, where IEntities (the moveable objects) are created. Each entity (robot, drone, and package), inherits from this IEntity class, which gives them all attributes such as location, name, direction, rotate, and details, along with functions with which to access these protected variables. When the simulation begins, SimulationModel calls upon the entity factories like DroneFactory and HumanFactory that extend IEntityFactory to create entities that exist on start like a helicopter that flies around, a human, and the drone.

When a delivery is scheduled, api calls in schedule.html, the main interface for scheduling packages, tell SimulationModel to create more entities. The package is then created with the inputted coordinates and with the name of the robot, and added to the entities list. The robot is created with its inputted coordinates and name as the owner of the package and put in the entities list too. With both the robot and the package, the delivery is pushed into a queue of scheduledDeliveries that the drone will then go through and finish by going to the package location with the beeline pathing algorithm, picking up the package (updating the package location on the simulation as the drone moves) and moving it with a user inputted pathing strategy (Dijkstras, BFS, DFS, AStar) which is stored on creation, then finally delivering it to the robot, where it does a celebration that the strategies have wrapped around them as a decorator. Finally, it moves on to the next delivery, and if it runs out, then the drone stays where it last delivered the package. 

![image](https://github.com/SussyGirlboss/Drone-Simulation/assets/136664014/cfce0014-82ad-4b4d-bd78-c6b2905a1892)
