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

### Integration of the social navigation algorithm in the Navigation component. 

The navigation component has changed in the last year, so it has been necessary to integrate in this component all the work done in my last GSOC. 

### Convex Hull to ConcaveHull 

### Free space with cost

### Taking into account the personal interactions in the clustering

### Go to person, accompany and follow person

### Detection of human blocking

### Detection of human "soft-blocking"

### Modification of DSR 

Once it has been detected if the person is blocking or soft-blocking the robot, it is necessary to add this information to the DSR, adding edges between the robot and the person.



***

### Posts
For a more detailed explanation of the work done during GSOC'18 visit the following links:
1. [Introduction: Social Navigation](/web/gsoc/2018/araceli_vega_magro/post1)
2. [Adaptive Personal Space](/web/gsoc/2018/araceli_vega_magro/post2)
3. [Modifications in the Navigation Agent](/web/gsoc/2018/araceli_vega_magro/post3)
4. [A flexible way to consider the personal spaces](/web/gsoc/2018/araceli_vega_magro/post4)
5. [Human blocking detector and other new functions](/web/gsoc/2018/araceli_vega_magro/post5)

### Content in GitHub
The work done during GSOC'18 can be found in my GitHub repository. It can be accessed in the following [link](https://github.com/aracelivegamagro/robocomp-shelly). 

Also, all the commits made for this project can be found in the following [link](https://github.com/aracelivegamagro/robocomp-shelly/commits/master). 


***
Araceli Vega Magro

