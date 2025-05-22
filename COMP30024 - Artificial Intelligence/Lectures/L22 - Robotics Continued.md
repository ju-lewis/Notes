
As sensors are not 100% reliable, and we're not always completely confident with the position of the robot in space, we can use *Bayes' Theorem* to compute the probabilities of obstacles actually being present in the space. 

Often **Incremental Bayes** will be used
- As we increase the number of measurements, the number of conditions in the formula grows
- Knowledge is accumulated with Incremental Bayes (not just episodic computations)


## Path Planning
Planning is typically done in *configuration space*

However, the configuration space is continuous - so path planning requires infinite time
- Hence we discretise the space

### Discretisation Strategies:
1. Cell Decomposition
2. Skeletonisation

### Voronoi Diagrams
Try to 'design' a line that joins all points that are equidistant from the edges in the configuration space

**Problem:**
- Doesn't scale well to higher dimensions

We can also create a mesh based on randomly sampling the configuration space



# Summary
- Two kinds of uncertainty in robotics (perception, action)
- We cannot interpret percepts without having assumptions about how they perform
- We use incremental Bayes theorem for correction



