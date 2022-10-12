<script setup>
let concentric = ["valuesPrimitive", "operatorsPrimitive", "operatorsAdvance"];
function forEach(array, script) {
  for (const child of array) {
    script;
  }
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
  let radials = document.querySelector(getElementID(event)).children;
  let radialDivisions = document.querySelector(getElementID(event)).children
    .length;
  let radialAngle = 360 / radialDivisions;
  let centerCoor = loadFunc();
  let terminus = document
    .querySelector(getElementID(event))
    .getBoundingClientRect();
  let radius = centerCoor.y - terminus.bottom;
  let position = {
    amount: radialDivisions,
    angle: radialAngle,
    radius: radius,
    forEach: radials,
  };
  return position;
}
function positionRails() {
  let h=loadFunc().x
  let k=loadFunc().y
  // need to define radius for each
  // need to itterate x and y
  
let rail 
//  Math.pow((x-h), 2)+Math.pow((y-k), 2)=Math.pow(radius, 2);
  // (x−h)2+(y−k)2=r2 
  console.log(k)
  console.log(rail)
}
</script>

<template>
  <button @click=" positionRails()">//onload</button>
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
