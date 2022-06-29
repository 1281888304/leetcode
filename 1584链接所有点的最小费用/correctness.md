step 1 : Explain the Union And Find
```` 
class UF{
    int[] parent;
    //edges number
    int count;
    
    public UF(int n){
        this.count=n;
        parent=new int[n];
        for(int i=0;i<n;i++){
            parent[i]=i;
        }
    }
    //find the parent of node x
    public int find(int x){
        while(parent[x]!=x){
            x=parent[x];
        }
        return x;
    }
    //node x's parent set to y's parent
    public void union(int x,int y){
        parent[find(x)]=find(y);
        count--;
    }
    //check if connected
    public boolean isConnected(int x,int y){
        return find(x)==find(y);
    }
}
````
1.1 for the constructor, the count shows how many points are not connected, and parent set all point's patent is itself

1.2 For the find method, the while loop is helping find node's root parents

1.3 for the union method, it make y's root parent became x's root parent

1.4 for the usConnected method, it use find method to check if x's root parent and y's root parent is same

step 2 build edges
```` 
//Kruskal‘s algorithm,sort all edges at first, and everytime find smallest edges
        //use priorityQueue find smallest edges
        PriorityQueue<int[]> pq = new PriorityQueue<>( (a,b)->a[2]-b[2] );
        //edges number
        int n=points.length;
        //make points to edge
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                int xi = points[i][0]; int yi = points[i][1];
                int xj = points[j][0]; int yj = points[j][1];
                // i j means points,use index to defind the point
                int[] edge = new int[]{i, j, Math.abs(xi-xj) + Math.abs(yi-yj) };
                pq.offer(edge);
            }
        }
````

2.1 the outer loop is 



