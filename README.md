Use this space to describe the function(s) that you wrote.

- ```path``` - 
```python
def path(network, source, dest):
    '''
    Purpose: Find a shortest path in network from source to
    destination.

    Parameters:
        network - adjacency list for a graph; dict
        source - the node to start the BFS run
        dest - the node where the desired path will end

    Return Value: a list containing a path from soruce to 
    destination.
    '''
```

Algorithm Overview

1. Initialize tracking dictionaries
- **visited** ← empty dictionary  
- **predecessor** ← empty dictionary  

For each `neighbor` in `network`:
- `visited[neighbor] = False`  
- `predecessor[neighbor] = None`

2. Handle the easy situation
If `source == dest`, return `[source]`.

3. Do the BFS setup
- Mark the source as visited:  
  `visited[source] = True`
- Initialize the queue with the source:  
  `Queue = [source]`

4. Do the BFS Loop
While the queue is not empty:

1. Remove the next node:  
   `current = Queue.pop(0)`

2. For each neighbor of `current`:  
   `for neighbor in network[current]:`

3. If the neighbor has not been visited:
   - Mark it visited  
     `visited[neighbor] = True`
   - Record its predecessor  
     `predecessor[neighbor] = current`

4. If the neighbor **is** the destination:
   - Start reconstructing the path  
     `path = [dest]`  
     `current = dest`
   - While `current != source`:
     - Move backward through predecessors  
       `current = predecessor[current]`
     - Append to path  
       `path.append(current)`
   - Reverse the path  
     `path.reverse()`
   - Return the path

5. Otherwise, add the neighbor to the queue:  
   `Queue.append(neighbor)`

- ```node_query``` -
  1. Run breadth-first search (BFS) on `network`, starting at `source`, to find the distance from `source` to every node.
  2. Create an empty list called `nodes_at_distance`.
  3. Check each node's distance from `source`.
  4. If a node's distance equals `dist`, add that node to `nodes_at_distance`.
  5. Return `nodes_at_distance`.
  
- ```is_connected``` - 
```python
def is_connected(network):
    '''
    Purpose: To determine if a graph is connected. That is does
    there exist a path between any pair of nodes in network?

    Parameter:
        network - graph adjacency list; dict
    
    Return Value:
        True - the graph is connected
        False - the graph is not connected
```
1. Handle the easy situation
If the network is empty, it is considered connected:
- `return True`

2. Choose a starting node
- Select any node from the network
- Run `bfs(network, start)` to figure out distances from this start node.
  - Returns two things:  
    - **distance**: a dictionary mapping nodes to shortest distance  
    - **node**: the last node visited (not used)

3. Check if all nodes are reachable
For each node in the network:
- If its distance is `float("inf")`, then the distance is infinity and it was never reached, the graph is **not** connected  
  - `return False`

4. If all nodes were reachable
- `return True`