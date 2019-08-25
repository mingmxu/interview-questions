**Question**:

 Your company built an in-house calendar tool called HiCal. You want to add a feature to see the times in a day when everyone is available.

To do this, you’ll need to know when any team is having a meeting. In HiCal, a meeting is stored as an object of a Meeting class with integer variables startTime and endTime. These integers represent the number of 30-minute blocks past 9:00am.
```
  public class Meeting {

    private int startTime;
    private int endTime;

    public Meeting(int startTime, int endTime) {
        // number of 30 min blocks past 9:00 am
        this.startTime = startTime;
        this.endTime   = endTime;
    }

    public int getStartTime() {
        return startTime;
    }

    public void setStartTime(int startTime) {
        this.startTime = startTime;
    }

    public int getEndTime() {
        return endTime;
    }

    public void setEndTime(int endTime) {
        this.endTime = endTime;
    }
}
```

For example:
```
new Meeting(2, 3);  // meeting from 10:00 – 10:30 am
new Meeting(6, 9);  // meeting from 12:00 – 1:30 pm
```
Write a method mergeRanges() that takes a list of multiple meeting time ranges and returns a list of condensed ranges.

For example, given:

  `[Meeting(0, 1), Meeting(3, 5), Meeting(4, 8), Meeting(10, 12), Meeting(9, 10)]`

your method would return:

  `[Meeting(0, 1), Meeting(3, 8), Meeting(9, 12)]`

Do not assume the meetings are in order. The meeting times are coming from multiple teams.

Write a solution that's efficient even when we can't put a nice upper bound on the numbers representing our time ranges. Here we've simplified our times down to the number of 30-minute slots past 9:00 am. But we want the method to work even for very large numbers, like Unix timestamps. In any case, the spirit of the challenge is to merge meetings where startTime and endTime don't have an upper bound. 

## Solution 1, if start/end time of meeting is from 0 to 16
```java
    //The core idea is, mark all the slots from input meetings, and scan the array to get merged meetings
    public static List<Meeting> mergeRanges(List<Meeting> meetings) {
        // merge meetings ranges
        boolean[] usedSlots = new boolean[16];
        for(Meeting m : meetings){
            for(int i=m.getStartTime(), e=m.getEndTime(); i<e; i++ ){
                usedSlots[i]=true;
            }
        }
        
        List<Meeting> merged = new ArrayList<>();
        for(int idx=0; idx<16;){
            if(!usedSlots[idx]){
                idx++;
                continue;
            }
            int f=idx;
            while(usedSlots[idx]) idx++;
            
            merged.add(new Meeting(f, idx));
        }


        return merged;
    }

```

## solution 2. if start/end time is infinite
```java
    //Sort all meetings by start time, and merge one-by-one based on 1/2/3 scenarios;
    public static List<Meeting> mergeRanges(List<Meeting> meetings) {
        if(meetings.size()<=1) return meetings;
        
        List<Meeting> merged = new ArrayList<>();
        Collections.sort(meetings, (i,j)->i.getStartTime() - j.getStartTime() );
        
        Meeting active = meetings.get(0);
        for(int idx=1, size=meetings.size(); idx<size; idx++){
            Meeting curM = meetings.get(idx);
            //1. not overlap
            if(curM.getStartTime() > active.getEndTime() ){
                merged.add(active);
                active=curM;
                continue;
            }
            //2, curM is part of active
            if(curM.getEndTime() < active.getEndTime() ){
                //do nothing
                continue;
            }
            //3. partial overlap
            if(curM.getStartTime() <= active.getEndTime() ){
                active.setEndTime( curM.getEndTime() );
                continue;
            }
        }
        //make sure the active one is added to result
        merged.add(active);

        return merged;
    }
```    
