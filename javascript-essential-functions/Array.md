# Useful Array Methods 

## Array.flat(level)
will flat out the array into single dimension array. if we have array inside array inside array then level_depth_integer specifies how many level deep we want to go to flat the array. by default its 1.

```
arr = [1,2,3,4,[5],[6, 7, 8, 9]];
arr.flat(level_depth_integer);
```

## Array.flatMap()
Unlike _flat()_ , flatMap lets us modify the data before flattening it. So we can perform any sorts of operations on it.
Below we have a highly irregular movie data which might be a mixture of different APIs (hence the irregularities)
It has array of movies, comma separated movies single movies and blank values as well.

We want to combine it to 1 array of movies
```
let movies = [
    'Inception',
    ['Titanic','Love from paris', 'Ocean 11'],
    'The Big Bang Theory',
    '',
    '    ',
    'Memento, The Bank Job, Money Heist',
    'Lady Bird',
    'Avengers, Batman, Ant-man',
    ['Platoon', ]
    
];

movies.flatMap((entry)=>{
    if(Array.isArray(entry))
    {
        return entry; //this will flatten that array and map each element of this array to the main array
    }
    else if(typeof entry === 'string' && entry.trim() === '')
    {
        return [];//means remove that element dont take it.
    }
    else{
        return entry.split(","); // split all the comma separated strings as different elements of array.
    }
})
```
