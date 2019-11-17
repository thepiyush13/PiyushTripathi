---
layout: post
title: Popular graph algorithms 
date: 2019-08-09 13:32:20 +0300
description: Comparing the performance of popular graph algorithms in dense and sparse graph network  # Add post description (optional)
img: icons/radar_plot.svg #i-rest.jpg # Add image post (optional)
fig-caption:  caption # Add figcaption (optional)
tags: [chrome, extension]
---



# Comparing the performance of popular graph algorithms in dense and sparse graph network

# Introduction
To implement a network routing protocol by modification of standard algorithms in order to find maximum bandwidth path. In this project we need to create a network graph and find the path between two nodes in a graph which has maximum capacity. These type of problems are important in networking, electronics and telecommunications and finding optimum solution within constraints can allow us to produce better and faster results for such problems.

# Problem Details
The main problem with this project is the fact that there should be an efficient way to find the solution without wasting too much memory/space or time. The graph/problem set could get very large, thus the proposed solution should be able to scale without producing incorrect results. First of all we need an efficient framework to work with graphical data. This framework should allow us to represent and manipulate graphical nodes in order to analyze the correctness and performance of our solution. The proposed solution should also take care of edge cases/corner cases and the solution should perform correctly even in cases where there is an anomaly and general deviation from expected input. The solution should also give most efficient path between two points among all the possible paths. This path would represent the path which can lead to maximum flow in a network. As per the solution we need to generate two type of Random graphs of 5000 vertices each:

# Grpahs

## Sparse Graph:
It contains exactly 6 degree vertices which means each vertex should be connected to 5 unique vertices in the graph.

## Dense Graph:
It is required that each vertex in the graph should be connected to at least 20% of other vertices. By calculating it, we deduce that each vertex should have at least 1000 degree.
In addition to above I am making sure that the graph does not contain self-loops or negative weight. I am also making sure the graph is sufficiently random so as to closely match our solution to the actual problem set.

# Technical Details
The programming language choice for this project was dependent on the ease of graph data structure representation and I found JAVA language to be suitable for this project. JAVA language offers object oriented functionality to organize the main problem in simpler problems. It also is memory efficient, widely available and supports IDE and debugging. I have used normal object oriented naming convention for the solution. Files are separated in logical classes and supported functions. I have tried to keep the code self-documented by providing meaning function and variable names. In addition to JAVA programming language, I have also used some graph plot and file operations library to visually represent the graph data structure. I have also used data charting tools to generate graphs for performance analysis.

# Solution Details
The project uses Object oriented programming methodology. I have created different classes to separate different algorithms. Each class handles a particular algorithm or a particular set of functions and this makes it easy for us to follow the project logic. Classes are initialized in the main runner class and give output based on the differently configured parameters. There are mainly 5 classes in the project. I will briefly explain each class and their respective purpose and functionality they offer.

 

## Edge
This class represents an edge between two nodes in a graph. The class contains vertices from which the edge is originating and the node to which the edge is connected. This class also holds the weight of the edge.

## Vertex
This Class represents a single vertex in a graph. The vertex consists of a uniquely identifiable name and the value stored in that vertex. For simplicity, I have kept the initial vertex weight to be same as the name.

## Graph
This is the main class which defines the underlying structure of a graph. A graph is made up of vertex and edges thus this class contains a list of edges and an adjacency list which stores the links from one vertex to another. The list is dynamic and keeps changing based on the type of graph we need. This class contains a variable V which denotes the maximum vertices the graph can have. Similarly the variable E represents the number of edges present in the graph. This graph contains a method addEdge which connects two vertex in the graph. It is important to have this functionality inside this class because in order to generate the graph, I am generating random vertices and connecting them together according to the constraints provided in the project. There is also a method in the class which confirms whether two vertices are connected to each other or not.

## GraphGenerator
As the name suggests this class generates the two kind of graph we need for the project. It contains methods that generates a dense graph (degree 1000). This method starts from 1st vertex goes till the last vertex and adds edges on the go. Before adding any new edge, the method makes sure to avoid already connected vertices, self-loops or vertices which are already filled (degree has reached maximum). After the check it adds required number of edges to each vertex. This continues till all the vertices have required number of edges connected to them. There is a slight optimization in this method due to practical reasons. As we are trying to generate truly random graph, it is difficult to ensure that the random generator always finds an available and valid vertex to add. This is due to the large data set and random probability distribution. Thus it could take very long period of time to get that particular vertex from pool of vertices in random fashion. As a solution to this problem I am allowing the random vertex finding loop to continue till a very long count is reached. If the loop is not able to generate the right vertex till these many iteration, I am breaking out of the loop and restarting the process to avoid infinite loop. The same logic is used in sparse graph generator, it is just that the degree of such graph will be less and it will complete is in lesser time compared to dense graph method. The class also contains and create path method which is created to fulfil the requirement of the project. The project statement required me to connect the source and destination vertex in case there is no path in original random graph. This class is divided in modular methods to make it easy to organize and understand the functionality. Overall this class is responsible for putting dense and sparse graph data together and making sure that the graph is valid data structure which can be worked upon by other classes.

## Dijkstra
This class is responsible for the solution of first part of the project. This class has a constructor which accepts a graph, a source vertex and a destination vertex and runs Dijkstra’s modified algorithm on the graph. It starts with marking all the vertices unmarked/unseen as it`s status. It also added positive infinity as their weight. After this step the method iterates through each vertex and depending on their edge weights added them to a list. I am using a sorted set for vertex as the list data structure for keeping the vertex sorted by their weight.

## DijkstraHeap
This class is very similar to Dijkstra class discussed above. The only difference is that instead of using a list of external vertices, this class uses a heap to maintain visited vertices list. There is a variable called heap Matrix which tracks the index of inserted elements in the heap. In the beginning we assign a status to each vertex which is unseen. This status denotes that we have not yet traversed this vertex. Then we go through each vertex one by one and assign a new status out which means the vertex is seen by is outside of connected list.IN the same loop we also assign parent of each vertex and distance from the source. We then loop through each item in the heap and depending on the status of the vertex we relax the vertex as mentioned in the Dijkstra’s standard algorithm. When this algorithm is complete, it marks all the vertex and finds path between source and destination. We have also used a max heap data structure for this purpose. In the max heap structure parent of any key will have value more than the child key. Thus we see that the topmost element of a max heap will always give us the largest value element in the heap. The class also contains heap helper function such as Heapify and InsetHeap and Delete Heap to provide additional operations on this data structure.

## Kruskal
This class used kruskal`s standard algorithm to find max bandwidth path between source and destination. This uses a concept of rank which is essentially the relative distance of a vertex. We start by assigning default parent and null rank to each of the vertex present in the graph. We then create a vertex array list. In this algorithm we create unions of found vertex and if any new vertex is found we add an edge to it. This class also uses union find methods to complete the functionality.

## Run
This is the main runner class for the entire project. It acts as an interface between different classes and creates objects as desired in the course of the operations. This class has a main method which is responsible for running various algorithms, keeping track of the time taken by them and finally printing these statistics to the console. As per the project description, we have to create 5 graph each of type dense and sparse and select 5 random source and destination pairs to test our algorithm. I have uses system nano function which accurately tracks how much time is spent between function calls, which effectively tells me the time taken by each of the algorithms. We start with our loop which runs 5 times generates two graphs dense and sparse in each iteration. Then we initialize a variable to store time and other details related to the algorithms. In each iteration we create 5 random source and destination pairs and feed them to different algorithms created in this project. This process applies both to the sparse and dense graph. At the end we print the time taken by each algorithm and the graph type it was passed. I am outputting the data in a slightly modified fashion because I am using the console output to generate time graphs for algorithm complexity visualization.

# Results and Diagrams
Results can be categorized in following categories:

## Sparse Graph
For Sparse graph the nodes had to be an exact number (6) thus it is important that each vertex only connects to exactly 5 other vertices. I have saved the graph data structure to a file to better understand the relationship between connected vertices. Here is a sample of generated graph:
Vertex()

Sample data

    vertex3199 vertex278(278) vertex 813(813) vertex 1419(1419) vertex 1937(1937) vertex 2832(2832) vertex 2935(2935) vertex 3197 vertex 499(499) vertex 1161(1161) vertex 2304(2304) vertex 2477(2477) vertex 2648(2648) vertex 3795(3795)

Visual representation

Sparse Grpah
We can see that the sparse graph has each vertex connected to exactly 5 other vertices which satisfies the requirement. It can also be noted that there are no duplicate vertices and self-loops in the graph. This was handled by the algorithm logic stated in the previous sections.

## Dense graph
The dense graph contains almost 1000 vertices connected to each of the vertex without self-loops or duplicate edges. The dense graph in some cases may not have exactly 1000 vertices because of constraints of the memory and respective workaround to counter that. However it is guaranteed that the graph has on an average 20% of other vertices connected to each of its vertex.
Vertex()

Sample data

    vertex3956 vertex195(195) vertex3189(3189) vertex3750(3750) vertex4458(4458) vertex4743(4743) vertex4638(4638)…………………… 1000

visual representation

Dense Grpah

Running all three algorithms do not produce any visible output as we are interested in the time taken by each. At the end we get the time complexity analysis of each of the three algorithms on console output. Below is the sample output received after running all the algorithms:

 

    GraphType	AlgoType	Time(milliseconds)

    Dense	Dijkstra	180.23882

    Dense	DijkstraWithHeap	631.52218

    Dense	Kruskal	2099.95518

    Sparse	Dijkstra	226.95219

    Sparse	DijkstraWithHeap	331.5543

    Sparse	Kruskal	35.01325

Finally we also calculate average time taken by each of the algorithms for all 5 types of graph we discussed, it is displayed in following fashion:

 

    GraphType	Dijkstra	Dijkstra with Heap	Kruskal)

    Avg Sparse(milliseconds)	64.43458	168.16116	13.83308

    Avg Dense(milliseconds)	191.25397	579.72298	1736.39182

 

# Performance Analysis
From the results we can see following results:

## Performance in Sparse graph
For sparse graph Dijkstra without heap takes about 65 ms to find max bandwidth path between given vertices. We can also see that the Dijkstra with heap takes even more time (168 ms) to find the same path. Thus it is clear that due to extra operations involved in the heap data structure manipulation it is not very efficient to use it in cases where the graph is sparse and very few edges are connected to each of the vertices. On the other hand kruskal’s modified algorithm outperforms both Dijkstra with and without heap. It takes only 14 ms to find the path. IT could be attributed to the logic of the algorithm which creates a maximum spanning tree and thus reduces additional comparisons significantly. Thus we can say that in sparse graph of smaller degree it is better to use kruskal’s algorithm to find maximum bandwidth paths between two vertices.

3
In the graph the horizontal axis represents the loop count and the vertical axis represents time taken in milliseconds.

## Performance in Dense Graph
It is very interesting to note that results change dramatically in case of the dense graph. We see that it kruskal has the worst performance in the dense graph of higher degree. Although it is given that any algorithm in the dense graph will traverse more nodes and take more time to find the max capacity path but even in that case the relative advantage of kruskal sharply decreased in dense graphs. The Dijkstra without heap performs best in case of dense graph and Dijkstra with heap performed somewhat in between Dijkstra without heap and kruskal (580 ms). Thus we can see that in case of dense graph with great number of edges connected to each of the vertices it better to use Dijkstra without heap to find max capacity path between given vertices.
4

# Conclusion
Thus we see that different algorithms perform differently for different types of graphs. For sparse graph kruskal’s algorithm is 4 times faster compared to Dijkstra but in the dense graph Dijkstra without heap algorithm is 9 time faster compared to kruskal’s algorithm. This shows that no algorithm is intrinsically faster or slower and could outperform or underperform depending on the situation. Thus our decision to use maximum capacity finding algorithm should greatly depend on the type and degree of the graph.

# Improvements
For future improvement I think we can introduce efficient data structures for each of the algorithms. Fox example instead of using union find we could introduce an algorithm which computes same process in less time. We can also improve underlying code structure for handling edge cases and avoid to compute where it is not required and the computing has already been done by previous computations. We can also look into improving the platform we use to run these algorithms as this will make memory management more efficient and with more computing power the overall time taken could be reduced.

# References
* Cormen, Thomas H. Introduction to algorithms. MIT press, 2009.
* Sedgewick, Robert. Algorithms in Java, Parts 1-4.
* Addison-Wesley Professional, 2002.Steier, David M, and Elaine Kant.
* “The Roles of Execution and Analysis in Algorithm Design.” Software Engineering, IEEE Transactions on 11 (1985): 1375-1386.
