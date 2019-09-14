# Question:
A crack team of love scientists from OkEros (a hot new dating site) have devised a way to represent dating profiles as rectangles on a two-dimensional plane.

They need help writing an algorithm to find the intersection of two users' love rectangles. They suspect finding that intersection is the key to a matching algorithm so powerful it will cause an immediate acquisition by Google or Facebook or Obama or something.

Two rectangles overlapping a little. It must be love.
Write a method to find the rectangular intersection of two given love rectangles.

As with the example above, love rectangles are always "straight" and never "diagonal." More rigorously: each side is parallel with either the x-axis or the y-axis.

They are defined as objects of Rectangle class:
```java
  public class Rectangle {

    // coordinates of bottom left corner
    private int leftX;
    private int bottomY;

    // dimensions
    private int width;
    private int height;

    public Rectangle() {}

    public Rectangle(int leftX, int bottomY, int width, int height) {
        this.leftX = leftX;
        this.bottomY = bottomY;
        this.width  = width;
        this.height = height;
    }

    public int getLeftX() {
        return leftX;
    }

    public int getBottomY() {
        return bottomY;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }
}
```
Your output rectangle should be a Rectangle object as well.

# Solution:
```java
    public static Rectangle findRectangularOverlap(Rectangle rect1, Rectangle rect2) {
        int minLeft=Math.min(rect1.getLeftX(), rect2.getLeftX());
        int maxRight = Math.max(rect1.getLeftX()+rect1.getWidth()
            , rect2.getLeftX()+rect2.getWidth() );
        if(maxRight - minLeft >= rect1.getWidth()+rect2.getWidth()){
            return new Rectangle();
        }
        
        int minLow = Math.min(rect1.getBottomY(), rect2.getBottomY());
        int maxHeight =  Math.max(rect1.getBottomY()+rect1.getHeight()
            , rect2.getBottomY()+rect2.getHeight() );
        if(maxHeight-minLow >= rect1.getHeight()+rect2.getHeight()){
            return new Rectangle();
        }
        
        // calculate the overlap between the two rectangles
        int leftx=Math.max(rect1.getLeftX(), rect2.getLeftX());
        int rightx=Math.min(rect1.getLeftX()+rect1.getWidth()
            , rect2.getLeftX()+rect2.getWidth() );
        
        
        int lowy=Math.max(rect1.getBottomY(), rect2.getBottomY());
        int highy =  Math.min(rect1.getBottomY()+rect1.getHeight()
            , rect2.getBottomY()+rect2.getHeight() );

        return new Rectangle(leftx, lowy
            , rightx-leftx, highy-lowy);
    }
```
