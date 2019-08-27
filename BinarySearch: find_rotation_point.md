# Question

I want to learn some big words so people think I'm smart.

I opened up a dictionary to a page in the middle and started flipping through, looking for words I didn't know. I put each word I didn't know at increasing indices in a huge array I created in memory. When I reached the end of the dictionary, I started from the beginning and did the same thing until I reached the page I started at.

Now I have an array of words that are mostly alphabetical, except they start somewhere in the middle of the alphabet, reach the end, and then start from the beginning of the alphabet. In other words, this is an alphabetically ordered array that has been "rotated." For example:

  String[] words = new String[]{
    "ptolemaic",
    "retrograde",
    "supplant",
    "undulate",
    "xenoepist",
    "asymptote",  // <-- rotates here!
    "babka",
    "banoffee",
    "engender",
    "karpatka",
    "othellolagkage",
};

Write a method for finding the index of the "rotation point," which is where I started working from the beginning of the dictionary. This array is huge (there are lots of words I don't know) so we want to be efficient here. 

# Solution
```java
    public static int findRotationPoint(String[] words) {
        //System.out.println(String.join(",",words));
        // find the rotation point in the array
        int from=0;
        int to=words.length-1;
        
        if(to<1) return 0;
        
        while(from<=to){
            int middle = (from+to)/2;
            //System.out.println("test:"+middle+words[middle]+", from="+from+words[from]+" to="+to+words[to]);
            
            //find the one, be careful of edge cases
            if( (middle==0 && words[middle+1].compareTo(words[middle])>0 )
                || (middle==words.length-1 && words[middle-1].compareTo(words[middle])>0 )
                || ( middle>0&&middle<words.length-1&& words[middle-1].compareTo(words[middle])>0 &&  words[middle+1].compareTo(words[middle])>0)
            ){
                //System.out.println("Find: "+words[middle]);
                return middle;
            } 
            
            //move right
            if( words[middle].compareTo(words[from])>=0  ){
                from=middle+1;
                //System.out.println("Move to right "+from);
            }else{
                //move left
                to=middle-1;
                //System.out.println("Move to left "+to);
            }
            //System.out.println("...");
        }

        return -1;
    }

```
