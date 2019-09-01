# Question
 Given an undirected graph ↴ with maximum degree ↴ DDD, find a graph coloring ↴ using at most D+1D+1D+1 colors.

For example:
First described by Robert Frucht in 1939, the Frucht graph is a 3-regular graph with 12 vertices, 18 edges, and no nontrivial symmetries.

This graph's maximum degree (DDD) is 3, so we have 4 colors (D+1D+1D+1). Here's one possible coloring:
The Frucht graph with legal coloring.

Graphs are represented by an array of NNN node objects, each with a label, a hash set of neighbors, and a color:
```java
import java.util.Collections;
import java.util.HashSet;
import java.util.Optional;
import java.util.Set;

public class GraphNode {

    private String label;
    private Set<GraphNode> neighbors;
    private Optional<String> color;

    public GraphNode(String label) {
        this.label = label;
        neighbors = new HashSet<GraphNode>();
        color = Optional.empty();
    }

    public String getLabel() {
        return label;
    }

    public Set<GraphNode> getNeighbors() {
        return Collections.unmodifiableSet(neighbors);
    }

    public void addNeighbor(GraphNode neighbor) {
        neighbors.add(neighbor);
    }

    public boolean hasColor() {
        return color.isPresent();
    }

    public String getColor() {
        return color.get();
    }

    public void setColor(String color) {
        this.color = Optional.ofNullable(color);
    }
}

GraphNode a = new GraphNode("a");
GraphNode b = new GraphNode("b");
GraphNode c = new GraphNode("c");

a.addNeighbor(b);
b.addNeighbor(a);
b.addNeighbor(c);
c.addNeighbor(b);

GraphNode[] graph = new GraphNode[] { a, b, c };
```

# Solution
```java
    public static void colorGraph(GraphNode[] graph, String[] colors) {
        if(graph.length==0) return;
        // create a valid coloring for the graph
        for(GraphNode g : graph){
            if(g.hasColor()) continue;
            Queue<GraphNode> queue = new LinkedList<>();
            queue.add(g);
            
            while(!queue.isEmpty()){
                GraphNode node = queue.poll();
                Set<String> usedColor=new HashSet<>();
                if(!node.hasColor()){
                    node.setColor(colors[0]);
                    usedColor.add(colors[0]);
                }else{
                    usedColor.add(node.getColor());
                }
                
                for(GraphNode n : node.getNeighbors()){
                    if(n==node) throw new RuntimeException();
                    
                    if(n.hasColor()){
                        usedColor.add(n.getColor());
                    }else{
                        for(String c : colors){
                            if(!usedColor.contains(c) && !existNeighborInColor(n, c) ){
                                n.setColor(c);
                                usedColor.add(c);
                                break;
                            }
                        }
                        queue.add(n);
                    }
                }
            }
        }
    }

    public static boolean existNeighborInColor(GraphNode node, String color){
        for(GraphNode n : node.getNeighbors()){
            if(n.hasColor() && n.getColor().equals(color) ){
                return true;
            }
        }
        
        return false;
    }
```
