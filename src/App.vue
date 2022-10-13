<script setup>
let data = [[], []];
let i;
let y;
let yCoor;
let x;
let xCoor;
let increments = [];
let positionData;
let convertToArray;
let concentric = ["valuesPrimitive", "operatorsPrimitive", "operatorsAdvance"];

function forEach(array, script) {
  for (let child of array) {
    script;
  }
}
function arrayToString(array) {
  for (i = 0; i < array.length; i++) {
    let string = "nameNO" + i;
    data[1].push(array[i]);
  }
  return data;
}
function convertToID(name) {
  let id = "#" + name;
  return id;
}
function getElementID(event) {
  let id = "#" + event.target.id;
  return id;
}
function loadFunc() {
  let center = document.querySelector("#centerButton").getBoundingClientRect();
  let xCoor = center.x;
  let yCoor = center.y;
  let width = center.width / 2;
  let height = center.height / 2;
  let centerCoor = {
    x: xCoor + width,
    y: yCoor + height,
    width: width,
    height: height,
  };
  return centerCoor;
}
function defineRadials(event) {
  let radials = document.querySelector(convertToID(event)).children;
  let radialDivisions = document.querySelector(convertToID(event)).children
    .length;
  let radialAngle = 360 / radialDivisions;
  let centerCoor = loadFunc();
  let terminus = document
    .querySelector(convertToID(event))
    .getBoundingClientRect();
  let radius = centerCoor.y - terminus.bottom;
  for (i = 0; i < radialDivisions; i++) {
    x = i;
    y = i;
    yCoor = centerCoor.y - Math.sqrt(Math.pow(-1*centerCoor.x, 2) + 2 * centerCoor.x * x + Math.pow(radius,2) - Math.pow(x,2));
    xCoor = centerCoor.x - Math.sqrt(Math.pow(-1*centerCoor.y, 2) + 2 * centerCoor.y * y + Math.pow(radius,2) - Math.pow(y,2));
    increments.push({x:xCoor, y:yCoor})
  }
  // let indexGetter = data[1].filter((position) => position == event)[0];
  let indexGetter = data[1].findIndex(item => item === event)
data[indexGetter].push(increments)
increments=[]
  let position = {
    amount: radialDivisions,
    angle: radialAngle,
    radius: radius,
    forEach: radials,
    positions: increments,
  };
  return position;
}
function positionRails() {
  let h = loadFunc().x;
  let k = loadFunc().y;
  let rail;
  let positions = arrayToString(concentric);
  // get all controlls
  for (i = 0; i < positions[1].length; i++) {
    convertToArray = defineRadials(positions[1][i]);

    //   position = {
    //   amount: radialDivisions,
    //   angle: radialAngle,
    //   radius: radius,
    //   forEach: radials,
    // };

    // data[0].push(positionData);
  }
  // return a postion array for each (matrix)
  // place childern in order according to position array
  // shift position based on scroll
  //
console.log(data[0])
}
</script>

<template>
  <button @click="positionRails()">//onload</button>
  <div class="flex flex-col" id="main">
    <div class="flex">
      <div
        id="headDiv"
        class="bg-slate-400 rounded-full aspect-square w-1/2"
      ></div>
      <div id="tearsleft" class="z-10"></div>
      <div id="tearsRight" class="z-10"></div>
    </div>
    <div id="bodyDiv" class="bg-slate-400 rounded-full aspect-square">
      <div class="bg-slate-400" id="valuesPrimitive">
        <button>0</button>
        <button>1</button>
        <button>2</button>
        <button>3</button>
        <button>4</button>
        <button>5</button>
        <button>6</button>
        <button>7</button>
        <button>8</button>
        <button>9</button>
      </div>
      <div class="bg-slate-400" id="operatorsPrimitive">
        <button>+</button>
        <button>-</button>
        <button>*</button>
        <button>/</button>
      </div>
      <div class="bg-slate-400" id="operatorsAdvance">
        <button>^</button>
        <button>(</button>
        <button>)</button>
        <button>√</button>
        <button>π</button>
      </div>
      <button class="rounded-full bg-slate-200 aspect-square" id="centerButton">
        =
      </button>
    </div>
  </div>
</template>

<style scoped>
* {
  padding: 0;
  margin: 0;
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
