#  Improving the Human-centered Robot Navigation Agent

My work during this GSOC has consisted in improving the robot navigation in environment with humans. The idea description is below:

RoboComp provides robots with the capability to behave in a socially acceptable manner. Particularly, the strategy followed in the Social Navigation Agent is based on the definition of regions where navigation is either discouraged or forbidden (personal spaces). These regions are related with the Proxemics, which defines spaces that humans mutually respects during an interaction. The navigation architecture combines the Probabilistic Road Map and the Rapidly-exploring Random Tree path planners and an adaptation of the elastic band algorithm to include the social behaviour. All of them are part of different RoboComp components. Considering the complexity of this task, the use of the current version of the social navigation agent is restricted, since it does not analyse, for instance, the human intentions during the robot navigation (do the human want to interact with the robot?) or the size of personal space depending of context (personal space should be different in a corridor than in a big room).

The task at hand here would be to integrate improvements in the existing RoboComp Social Navigation Agent. In a future version of this agent, more complex situations will be taking into account, such as human intention analysis and/or adaptive personal spaces. A typical case of use would be that of a group of humans walking in different environments while the robot performs a task. All these simulations would be made using RCIS (RoboComp InnerModel Simulator)


## The initial proposal

RoboComp works with a Deep State Representation in order to represent the world, robot and humans in the environment. Social behavior in RoboComp is based on proxemic and  it defines areas where navigation is forbidden. These comfort regions are static, that is, all humans generate the same personal space independent of the environment, spatial context, etc.
 
My proposal consisted on transform the fixed personal space used in Robocomp into an adaptive space, depending of the spatial context (there is difference, for instance, between a narrow corridor and a room). The main idea was to change the values that defines the personal space function in order to adapt the personal space to allow the robot to navigate around the person without problems, adapting it to the spatial context. Besides, I wanted to extend the social navigation agent, including other typical social behaviors: crossing people in corridors, approaching to humans in human-robot interaction, etc.   

Due to the changes made in the navigation component of the robot in the last year, it has not been necessary to modify the personal space of humans in the initial way i have thought, since it has been possible to achieve the goal of making this space more flexible in another way, that it will be explained next. 

***

## Work done 

The work done during this GSOC is summarized below. For a more detailed description, the posts are attached at the end of the page.

### Integration of the social navigation algorithm. 

The navigation component has changed in the last year, so it has been necessary to integrate in this component all the work done in my last GSOC. The free space graph and the planification algorithm have changed, reason why some modifications had to be performed. 

In first place, the free space graph is now a regular graph, formed by a set of free or occupied points. It has been necessary to set as occupied the points contained in the personal space of humans.

Also, the planning algorithm has changed. Before it was used the PRM planner but now the Dijkstra algorithm is used, which searches for the shortest path from the initial position to the destination based only on the free space graph. Thanks to that, it is not longer necessary to include planes in the edges of the personal space.

### ConvexHull to ConcaveHull 

Before it was needed less number of points to represent the polylines because the insertion of planes. To reduce the number of points the ConvexHull was calculated.

After the changes made in the component the number of points it is not important, reason why the way the polyline is obtained has changed. the ConcaveHull is calculated to obtain the points of the polyline. With the ConcaveHull the form of the polyline is more accurated.

### Free space with cost

This is one of the most important contributions in this GSOC, as it allows to get a more flexible way to treat the personal spaces of humans.

The free space graph is represented by a set of nodes that are considered free or occupied. These nodes also have a parameter that represent the cost of each point. The robot plans the shortest path between the points of the graph taking into account the cost. Three personal spaces has been considered: intimate space, personal space and social space. The cost of each area has been increased in order that, when the robot plans the shortest route, it will move away from the person, as crossing the personal and social spaces will mean that the path will be longer.

This is a flexible way to adapt the spaces to the environment. If the robot doesn’t have enouh space to navigate, for example in a corridor, if won’t be blocked, but it will navigate through the personal space even if the cost is higher. Besides, it will never cross the intimate area as it is always considered as occupied.


### Taking into account the personal interactions in the clustering

The navigation algorithm has been modified in order to cluster the people only if they are interacting.  The human agent adds interacting links between persons when they are interacting. The navigation algorithm reads these links and separates people who are interacting from those who are not.  This allows the robot to navigate between people who are not interacting, facilitating the navigation, as no cluster is done.

### Other functions implemented

New functions have been implemented, such as go to person, which allows the robot to approach a certain person given his id in order to interact with it. The accompany function sends the robot next to the person each time it moves. The same thing does the function follow, in this case sending it behind the person. Finally, the pass on right function has been integrated, which creates another gaussian curve turned to the left that makes the robot planify a path passing on the right of the person.

### Detection of human blocking and "soft-bockling"

There can be situations where the robot can not pass because the personal space of humans blocks the path. In this situations, the robot should ask colaboration to pass. To this aim, a function which check if there are humans blocking the path has been created. It uses a empty free space graph to check if the robot can pass without human spaces on it, if it does, it means that the path is blocked by a human. To detect which human blocks the path, the personal spaces of each human present in the environment is inserted one by one. When the robot can not find a path, it means that the last space inserted in the graph is the one which blocks the robot trajectory. In this cases the person blocks the path.

There also can be situations where the robot can pass but it does it by getting close to the person, that is, going through his personal space. In this cases, the robot must approach the person and ask permission to pass. To detect if the robot is getting too close to a person, it is calculated if the planned path goes through the personal space of each human. If it does, the person is soft-blocking the path.

#### Modification of DSR 

Once it has been detected if the person is blocking or soft-blocking the robot, it is necessary to add this information to the DSR, adding edges between the robot and the person. To do this, a list of the previous edges between the robot and the person is stored. When this list changes, the old edges are removed and the new ones are inserted.

***

### Posts
For a more detailed explanation of the work done during GSOC'18 visit the following links:
1. [Introduction: Social Navigation](/web/gsoc/2018/araceli_vega_magro/post1)
2. [Adaptive Personal Space](/web/gsoc/2018/araceli_vega_magro/post2)
3. [Modifications in the Navigation Agent](/web/gsoc/2018/araceli_vega_magro/post3)
4. [A flexible way to consider the personal spaces](/web/gsoc/2018/araceli_vega_magro/post4)
5. [Human blocking detector and other new functions](/web/gsoc/2018/araceli_vega_magro/post5)
6. [Modifications in the DSR](/web/gsoc/2018/araceli_vega_magro/post6)

### Content in GitHub
The work done during GSOC'18 can be found in my GitHub repository. It can be accessed in the following [link](https://github.com/aracelivegamagro/robocomp-shelly). 

Also, all the commits made for this project can be found in the following [link](https://github.com/aracelivegamagro/robocomp-shelly/commits/master). 


***
Araceli Vega Magro

