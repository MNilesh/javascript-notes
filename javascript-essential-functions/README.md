
## Array Methods:
### Array.flat(level)
will flat out the array into single dimension array. if we have array inside array inside array then level_depth_integer specifies how many level deep we want to go to flat the array. by default its 1.

```
arr = [1,2,3,4,[5],[6, 7, 8, 9]];
arr.flat(level_depth_integer);
```


## Useful DOM Methods
### ev.composedPath()
this method returns returns an array of all the elements inside which the clicked element is present. 
this method is present in the event object
```ev.composePath()```
