# Question



My cake shop is so popular, I'm adding some tables and hiring wait staff so folks can have a cute sit-down cake-eating experience.

I have two registers: one for take-out orders, and the other for the other folks eating inside the cafe. All the customer orders get combined into one list for the kitchen, where they should be handled first-come, first-served.

Recently, some customers have been complaining that people who placed orders after them are getting their food first. Yikes—that's not good for business!

To investigate their claims, one afternoon I sat behind the registers with my laptop and recorded:

    The take-out orders as they were entered into the system and given to the kitchen. (takeOutOrders)
    The dine-in orders as they were entered into the system and given to the kitchen. (dineInOrders)
    Each customer order (from either register) as it was finished by the kitchen. (servedOrders)

Given all three arrays, write a method to check that my service is first-come, first-served. All food should come out in the same order customers requested it.

We'll represent each customer order as a unique integer.

As an example,
```
  Take Out Orders: [1, 3, 5]
 Dine In Orders: [2, 4, 6]
  Served Orders: [1, 2, 4, 6, 5, 3]
```
would not be first-come, first-served, since order 3 was requested before order 5 but order 5 was served first.

But,
```
  Take Out Orders: [1, 3, 5]
 Dine In Orders: [2, 4, 6]
  Served Orders: [1, 2, 3, 5, 4, 6]
```
would be first-come, first-served.


# Solution 1. two-pointers move
```java
    public static boolean isFirstComeFirstServed(int[] takeOutOrders, int[] dineInOrders, int[] servedOrders) {
        if(takeOutOrders.length+dineInOrders.length != servedOrders.length){
            return false;
        }

        // check if we're serving orders first-come, first-served
        for(int i1=0, i2=0, i3=0; i3<servedOrders.length; ++i3){
            if(i1<takeOutOrders.length && takeOutOrders[i1]==servedOrders[i3] ){
                i1++;
                continue;
            }
            if(i2<dineInOrders.length && dineInOrders[i2]==servedOrders[i3] ){
                i2++;
                continue;
            }
            return false;
        }

        return true;
    }
```
