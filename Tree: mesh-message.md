# Question
 You wrote a trendy new messaging app, MeshMessage, to get around flaky cell phone coverage.

Instead of routing texts through cell towers, your app sends messages via the phones of nearby users, passing each message along from one phone to the next until it reaches the intended recipient. (Don't worry—the messages are encrypted while they're in transit.)

Some friends have been using your service, and they're complaining that it takes a long time for messages to get delivered. After some preliminary debugging, you suspect messages might not be taking the most direct route from the sender to the recipient.

Given information about active users on the network, find the shortest route for a message from one user (the sender) to another (the recipient). Return an array of users that make up this route.

There might be a few shortest delivery routes, all with the same length. For now, let's just return any shortest route.

Your network information takes the form of a hash map mapping username strings to an array of other users nearby:
```java
  Map<String, String[]> network = new HashMap<String, String[]>() {{
    put("Min",     new String[] { "William", "Jayden", "Omar" });
    put("William", new String[] { "Min", "Noam" });
    put("Jayden",  new String[] { "Min", "Amelia", "Ren", "Noam" });
    put("Ren",     new String[] { "Jayden", "Omar" });
    put("Amelia",  new String[] { "Jayden", "Adam", "Miguel" });
    put("Adam",    new String[] { "Amelia", "Miguel", "Sofia", "Lucas" });
    put("Miguel",  new String[] { "Amelia", "Adam", "Liam", "Nathan" });
    put("Noam",    new String[] { "Nathan", "Jayden", "William" });
    put("Omar",    new String[] { "Ren", "Min", "Scott" });
    ...
}};
```
For the network above, a message from Jayden to Adam should have this route:

  { "Jayden", "Amelia", "Adam" }

# Solution
```java
    public static String[] getPath(Map<String, String[]> graph, String startNode, String endNode) {
        if(startNode.equals(endNode)) return new String[]{startNode};
        
        // find the shortest route in the network between the two users
        if( !graph.containsKey(startNode) || !graph.containsKey(endNode) ){
            throw new RuntimeException();
        }
        
        Queue<NodeWithPath> queue = new LinkedList<>();
        NodeWithPath sPath = new NodeWithPath(startNode);
        sPath.path.add(startNode);
        queue.add(sPath);
        
        Set<String> visited = new HashSet<>();
        visited.add(startNode);
        
        while(!queue.isEmpty()){
            NodeWithPath n = queue.poll();
            for(String next : graph.get(n.value) ){
                if(visited.contains(next)){
                    continue;
                }
                visited.add(next);
                
                NodeWithPath nextNode = new NodeWithPath(next);
                nextNode.path.addAll(n.path);
                nextNode.path.add(next);
                
                if(next.equals(endNode)){
                    //find
                    return nextNode.path.toArray(new String[]{});
                }else{
                    queue.add(nextNode);
                }
            }
        }
        
        return null;
    }



    public static class NodeWithPath{
        public String value;
        public List<String> path = new ArrayList<>();
        
        public NodeWithPath(String value){
            this.value=value;
        }
    }
```
