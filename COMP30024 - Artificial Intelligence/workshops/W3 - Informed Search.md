

# 1. Heuristics
**1a.** If $h(\sigma) = -g(\sigma)$, GBFS will always pick the 'deepest' node it can reach
- As path cost increases, the heuristic for that node decreases
- Depth-first search

**1b.** $w: f(\sigma)=(2-w)g(\sigma)+wh(\sigma)$

For $w=0$, $f(\sigma)=(2)g(\sigma)$
- We would get uniform cost search (avoid expanding expensive paths)

For $w=1$, $f(\sigma) = (1)g(\sigma)+h(\sigma)$
- This is A* search; consider both path cost and heuristic estimate - provided $h(\sigma)$ is admissible

For $w=2$, $f(\sigma)=2h(\sigma)$
- This is greedy best first search; only consider the heuristic from the current node


$f(\sigma)$ is optimal for values of $w$ between 0 and 1


# 2. Generation vs. Expansion

**2a.** 
The goal test should be mostly performed on *expansion*, except in a few cases. This is because most algorithms generate all child nodes of the current node immediately, and may choose non-optimal solutions as a result (even if they are optimal search algorithms, since they will not expand that node immediately).


**2b.** 

On state expansion:
1. Expand Sibiu
2. Goal test Sibiu
3. Expand Rimnicu Vilcea
4. Goal test Rimnicu Vilcea
5. Expand Fagaras
6. Goal test Fagaras
7. Expand Pitesti
8. Goal test Pitesti
9. Expand Bucharest
10. Goal test Bucharest

Cost to Bucharest: 278

On state generation:
1. Expand Sibiu
2. Goal test Rimnicu Vilcea and Fagaras
3. Expand Rimnicu Vilcea
4. Goal test Pitesti
5. Expand Fagaras
6. Goal test Bucharest

Cost to Bucharest: 310



# 3. Tracing A* Search

1. Expand Lugoj
2. Generate Mehadia (g(x) = 70, h(x) = 280) and Timisoara (g(x) = 111, h(x) = 320)
3. Expand Mehadia
4. Generate Drobeta (g(x) = 145 h(x) = 240)
5. Expand Timisoara
6. Generate Arad (g(x) = 229 h(x) = 360)
7. Expand Drobeta
8. Generate Craiova (g(x) = 265 h(x) = 138)
9. Expand Craiova
10. Generate Pitesti (g(x) = 403 h(x) = 0)
11. Expand Pitesti

# 4. Gridlock

**4a.**
The state space size

**4b.**
For each of the $n$ vehicles we can theoretically make the choices:
- up
- down
- left
- right
- stay put
These movement options can either be to an adjacent square, or over a stationary car
And because we make one of these 5 decisions for all of the $n$ vehicles we can make:
$$5\times5\times...\times5$$
where the multiplication is repeated $n$ times.
So our branching factor is $5^n$

**4c.**
A non-trivial admissible heuristic could assume that the vehicle is always able to move directly towards its goal state. In other words we can use *manhattan distance*.


