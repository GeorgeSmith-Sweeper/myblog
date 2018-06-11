---
layout: post
title: "TIL: Using spread with findIndex"
date:  2018-06-07
comments: true
categories: jekyll update
---

![Berry jam being spread on a piece of toast with a knife]({{ GeorgeSmith-Sweeper.github.io }}/assets/jam_spread.jpg){:class="img-responsive"}


Today I learned that its possible, and fairly easy to locate a single unique item in an array, remove it, and return a new array without all without side effects. I'm going to walk you through the process using a hypothetical example.

Lets say that we're developers working at a parking garage (extremlly glamorous and exciting). The parking garage owner has a fully automated system that adds cars to the inventory, and assigns them a unique id. Esentially we'll have an array filled with "car" objects.

```javascript

let garage = [
  {id: 529, make: 'Jeep', model: 'Cherokee'},
  {id: 700, make: 'Ferrari', model: 'Laferrari'},
  {id: 839, make: 'Subaru,' model: 'STI'},
  {id: 912, make: 'Buick,' model: 'Continental'},
  {id: 43, make: 'Tesla,' model: 'Model 3'}
]

```
The garage owner wants us to create a simple function that updates the state of the garage (it's inventory) whenever a car leaves the facility. Luckily for us we can use `findIndex`, and `...` (spread) along with the cars unique `id` to get the job done easily. We'll make a function called remove car, and pass it the id of the car, and the garage array.

Lets say we wanted to remove the car with the id of `912` from the `garage` array. The first thing we would need to do is figure out where id 912 resides within the array. `findIndex` will loop though each element (car object) until it finds the one that matches the provided id. Once the id is found, `findIndex` will return the location where the match was made. We get index `3`.

```javascript

const newGarageState = removeCar(912, garage);

const removeCar = (carId, garage) => {
  // find the index of the car we want to remove
  const carIndex = garage.findIndex(car => car.id === carId);
}

```

Once we have the index of the car that we'll be removing, can create a new array `newGarage` with the single car excluded. We start by using `.slice` to find all of the cars before, and after the car that we're going to remove. Once we have these arrays, we can spread them into an array literal `[]` and return it!

```javascript

const removeCar = (carId, garage) => {
  const carIndex = garage.findIndex(car => car.id === carId);

  const carsBeforeIndex = garage.slice(0, carIndex);
  const carsAfterIndex = garage.slice(carIndex + 1);

  const newGarage = [...carsBeforeIndex, ...carsAfterIndex];

  return newGarage;
};
```
