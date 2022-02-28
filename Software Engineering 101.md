# Software Architectures
## Overview
1. Layered
1. Client Server
1. Master - Slave
1. Peer to Peer
1. Model View Controller
1. Event Driven

## 1. Layered Architecture
* **Presentation Layer:** This layer is all about user interface
* ...
* **Business Layer**
* ...
* **Persistence Layer**
* ...
* **Database Layer:** This layer deals with the data and database transactions.  

The main purpose of this architecture is to isolate the layers from the others, i.e. Separations of concerns, the number of layers varies.  
There are components in each layer and data in database layer, request chains from top to bottom, response chains from bottom to top. A layer cannot access the layers other than the one its below and above directly.  
Sometimes accessing a layer through the layer between it is redundant, in this case, we can make the design to allow overpassing this layer. Such a layer is called an open layer, otherwise it is a closed layer.  

|  Cons | Pros |  
| ---: | :--- |  
| Sinkhole Antipattern | High Testability |  
| Low Ease of Deployment | Separation of concerns is good applied |  
|Low Performance |  |


## 2. Client - Server Architecture
Basically it consists of requests from client and responses from the server. First example that comes to mind for this architecture is the structure of internet web sites. 

## 3. Master - Slave Architecture
In this architecture, the master assigns the problem to various numbers of slaves to solve. Each slave appliest its own solution to the problem parallelly and comes up with a result. Then, the master combines or chooses the solution to form the result.

## 4. Peer to Peer Architecture

The best example to this architecture is the file sharing systems. There is no centralized system, every peer is a client and server at the same time. The burden is shared among the peers. 

### 4.1. Pros
- Adding or removing a peer is easy
- Economic

### 4.2. Cons
- A problem (i.e. virus) spreads easily

## 5. MVC (Model View Controller)

This architecture is a good example of separation of concerns principle.
- Model keeps the data, no logic, it is not aware of View
- View presents and shows the content, not aware of the Model
- Controller in communication with the other two and it organizes the flow while doing the logic.

## 6. Event Driven Architecture

There are two topologies in this Architecture
### 6.1. Mediator Topology
In this topology, there is one central mediator which is responsible to take the initial event and distribute its sub-events to event channels. Each event channel has an event processor. The mediator does not do logic, but controls and organizes the event and steps, for example, if a processor needs results of another step, mediator takes the results from other processor and provides to this processor.

### 6.2. Broker Topology

There is no central event mediator. In this topology there is no organizer, event processors run paralelly. They process the steps and listens the event channel at the same time, after all processors stop listening and processing, the main event is completed.  
It is an asynchronous architecture

### 6.3. Pros and Cons
- Agility: High
- Ease of Deployment: High
- Testability: Low
- Performance: High
- Scalibility: High
- Ease of Development: Low

# Software Developing Paradigms

## 1. OOP (Object Oriented Programming)
###  Foundations
1. **Abstraction:** We can prepare and get a coffee using a coffee machine, we don't need to know how to make a coffee.
1. **Encapsulation:** Hide and protect the properties from outside.
1. **Inheritance:** 
1. **Polymorphism:** A reference can keep any of its sub-classes.

## 2. Data Oriented Design
Focuses on hardware performance. It proposes to keep data in simple structures like arrays and don't use tree like structures. For example, it proposes to consider cache hit ratio while designing the structure to keep our data.

## 3. Functional Programming
Does not keep the data in the objects since it doesn't have objects. Functional programming does not support data manipulation as a result, there is no operations like array editing, file writing, deleting or updating.
# Measuring Quality of the Software
## 1. Cyclomatic Complexity
It is a measure of complexity of a code (a method, a class, or a whole program). A high cyclomatic complexity value means spaghetti code. There are formulas to calculate. One variation is,  
$$Cyclomatic\space Complexity = E - N + 2P$$
E: Edges between nodes  
N: Nodes  
P: Components

 A software with high complexity causes high maintenance costs, more difficult testing and a larger team of designers. 
 
 ## 2. Halstead's Complexity Measures
 
 
$n_1$: Number of distinct(unique) operators  
$n_2$: Number of distinct(unique) operands  
$N_1$: Number of total operators  
$N_2$: Number of total operands

$n=n_1 + n_2$  
$n$ = Program vocabulary

$N = N_1 + N_2$  
$N$: Program Length

$\hat N = n_1 \log_2 n_1 + n_2 \log_2 n_2$  
$\hat N$: Calculated estimated program length  

$ V = N \log_2 n$  
$V$: Volume  (Should be: 20 < V < 1000)

$D = \frac {n _ 1}{2} \times  \frac {N_2}{n_2}$  
$D$: Difficulty  (Measure of how error prone)

$E =  D \times V$  
$E$: Effort (How difficult to applicate and understand)  

$T = \frac{E}{18}seconds$  
$T$: Time requried to program  

$B = \frac{E^{\frac{2}{3}}}{3000}$  
$B$: Number of delivered bugs

**Example:***  
```C
main()
{
    int a, b, c, avg;
    scanf("%d %d %d", &a, &b, &c);
    avg = (a + b + c) / 3;
    printf("avg = %d", avg);
}
```
The unique operators are ***main, (), {}, scanf, int, &, =, +, /, printf, ,, ;***  
The unique operands are ***a, b, c, avg, "%d %d %d"*** and ***"avg = %d"***  
$n_1 = 12, n_2=7, n=19$  
$N_1 = 27, N_2=15, N=42$  
$\hat N = 12 \log _ 2 12 + 7 \log _ 2 7 = 62.67$  
$V = 42 \log 19 = 178.4$  
$D = \frac{12}{2} \frac{15}{7} = 12.85$  
$E = 12.85 * 178.4 = 2292.44$  
$T = \frac{2292.44}{18} = 127.357 secs$  
$B = \frac{2292.44^{\frac{2}{3}}}{3000} = 0.05$    

# Software Testing
Box Approach will be discussed in this section.

## 1. White Box
The intend is to test internal structures or workings of an application.
- **Unit test:** Test functions if they work properly
- **Integration tests**
    - **Big Bang Approach:** Don't test until all modules are ready. In this approach, QA team wait until all modules are ready.Its good for smaller systems but,in larger systems, sometimes it is hard to find in which modules the problems are.
    - **Incremental Approach:** Place mock modules to represent the modules which are not ready and test modules which are ready as the system is being developed.
- **Code coverage:** It represents the percentage of the code that we have tested. How much of the code executed while testing.
## 2. Black Box
In this approach, we have the inputs and the outputs. The system is a blackbox which we don't know about inside structure.
- Functionality tests, check the functions of the system if they work as expected.
- Non-functional tests, performance on various conditions or platforms. Compatibility tests over various platforms.
- Regression tests, after applying a solution or improvement check if it has been effective.

### Usability Tests
- Easy to use?
- Easy to learn?
- Efficient?
- Memorable?
### Load Test
Put demand on the system and measure the response. For example, for testing a server, write bots and send large amount of requests.
### Compatibility
Test the behaviours or responses on various platforms and see how compatible on those.

### Stress Testing
Test the system out of standards, push to the limits.

### Scalability Testing
See what are the limits of your system.

# Documentation
The knowledge need to be transferrable, hence docunmentation is necessary.
- Doxygen is a documentation application
- Documentation is not adding commentlines everywhere, the code should be self-explanatory.  
[Code As Design](https://www.developerdotstar.com/mag/articles/reeves_design_main.html) an article 
about documentation.

# Characteristics of a Software
- Minimum Complexity
    - Simple
    - Easy to understand
    - Isolation Level Should be high, components should be independant.
- Ease of Maintenance
    - Design should be self-explanatory
- Loose Coupling
    - Abstraction
    - Encapsulation
    - High Cohesion  
    - With loose coupling these will be lower
        - Cost of Integration
        - Cost of Testing
        - Cost of Maintenance
- Extensibility
    - In an extensible system, a piece of system can be changed without effecting the rest.
- Portability
    - Easily move or adapt to another platform.  
    
We need to establish a reasonable balance between all these characteristics since we won't be able to assure all.
    