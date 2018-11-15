---
title: "Map Reduce and Filter"
date: 2018-11-15T21:24:18+05:30
tags : [
    "Javascript",
    "Interview",
   ]
---

# Map Reduce and Filter

## .map()

To modify an array or it's objects

map receives a callback as an argument. That callback is then given the current value of the iteration, the index of the iteration and the original array from which map was called

```
const arr = [1,2,3,4,5];
const newArray = arr.map(i => i*10);
// return a new array with all value as multiple of 10;
```

```
var officers = [
  { id: 20, name: 'Captain Piett' },
  { id: 24, name: 'General Veers' },
  { id: 56, name: 'Admiral Ozzel' },
  { id: 88, name: 'Commander Jerjerrod' }
];

var officersIds = officers.map(function (officer) {
  return officer.id
});

or 

const officersIds = officers.map(officer => officer.id);

```
The callback runs for each value in the array and returns each new value in the resulting array.

---
## .reduce()

Runs a callback for each element of an array.The callback now receives the accumulator (it accumulates all the return values. Its value is the accumulation of the previous returned accumulations), the current value, the current index and finally the whole array.

```
var obj = songs.reduce(function (acc, currValue) {
  var artist = currValue.artist;
  var artistCount = acc[artist] ? acc[artist] + 1 : 1;
  
  var newObj = {};
  newObj[artist] = artistCount;
  
  return Object.assign(acc, newObj);
}, {});

// ES6
const obj = songs.reduce((acc, currvalue) => {
  const artist = currValue.artist;
  const artistCount = acc[artist] ? acc[artist] + 1 : 1;
  
  return {
    ...acc,
    [artist]: artistCount,
  };
}, {});

console.log(obj); 
```

```
const numbers = [2,10,11,5,16];

var sum = numbers.reduce(function (acc, currValue) {
  return acc + currValue;
}, 0);

// ES6
const sum = numbers.reduce((acc, currValue) => {
  return acc + currValue;
}, 0);


```

```
var pilots = [
  {
    id: 10,
    name: "Poe Dameron",
    years: 14,
  },
  {
    id: 2,
    name: "Temmin 'Snap' Wexley",
    years: 30,
  },
  {
    id: 41,
    name: "Tallissan Lintra",
    years: 16,
  },
  {
    id: 99,
    name: "Ello Asty",
    years: 22,
  }
];

var totalYears = pilots.reduce(function (accumulator, pilot) {
  return accumulator + pilot.years;
}, 0);

or

const totalYears = pilots.reduce((acc, pilot) => acc + pilot.years, 0);


```



## .filter()

As name dictates

```
var pilots = [
  {
    id: 2,
    name: "Wedge Antilles",
    faction: "Rebels",
  },
  {
    id: 8,
    name: "Ciena Ree",
    faction: "Empire",
  },
  {
    id: 40,
    name: "Iden Versio",
    faction: "Empire",
  },
  {
    id: 66,
    name: "Thane Kyrell",
    faction: "Rebels",
  }
];

var rebels = pilots.filter(function (pilot) {
  return pilot.faction === "Rebels";
});
var empire = pilots.filter(function (pilot) {
  return pilot.faction === "Empire";
});

or

const rebels = pilots.filter(pilot => pilot.faction === "Rebels");
const empire = pilots.filter(pilot => pilot.faction === "Empire");

```

Here, the callback needs to return either true or false. If it returns true then the array keeps that element and if it returns false the element is filtered out.


[Examples](https://medium.com/@joomiguelcunha/learn-map-filter-and-reduce-in-javascript-ea59009593c4)