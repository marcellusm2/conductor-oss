# Directed Acyclic Graph (DAG)
## What is a Directed Acyclic Graph (DAG)?
Conductor workflows are directed acyclic graphs (DAGs). But, what exactly is a DAG?

To understand a DAG, we'll walk through each term (but not in order):

### Graph

A graph is "a collection of vertices (or point) and edges (or lines) that indicate connections between the vertices."  

By this definition, this is a graph - just not exactly correct in the context of DAGs:

![pirate vs global warming graph](pirate_graph.gif)

But in the context of workflows, we're thinking of a graph more like this:

![a regular graph (source: wikipedia)](regular_graph.png)

Imagine each vertex as a microservice, and the lines are how the microservices are connected together. However, this graph is not a directed graph - as there is no direction given to each connection.

### Directed

A directed graph means that there is a direction to each connection. For example, this graph is directed:

![directed graph](directed_graph.png)

Each arrow has a direction, Point "N" can proceed directly to "B", but "B" cannot proceed to "N" in the opposite direction.  

### Acyclic

Acyclic means without circular or cyclic paths.  In the directed example above,  A -> B -> D -> A is a cyclic loop.  

So a Directed Acyclic Graph is a set of vertices where the connections are directed without any looping.  DAG charts can only "move forward" and cannot redo a step (or series of steps.)

Since a Conductor workflow is a series of vertices that can connect in only a specific direction and cannot loop, a Conductor workflow is thus a directed acyclic graph:

![Conductor Dag](dag_workflow2.png)

### Can a workflow have loops and still be a DAG?

Yes. For example, Conductor workflows have Do-While loops:

![Conductor Dag](dag_workflow.png)

This is still a DAG, because the loop is just shorthand for running the tasks inside the loop over and over again.  For example, if the 2nd loop in the above image is run 3 times, the workflow path will be:

1. zero_offset_fix_1
2. post_to_orbit_ref_1
3. zero_offset_fix_2
4. post_to_orbit_ref_2
5. zero_offset_fix_3
6. post_to_orbit_ref_3

The path is directed forward, and the loop just makes it easier to define the workflow.
