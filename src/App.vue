<script setup>
let data = [[], []];
let xValues = [];
let yValues = [];
let i;
let h;
let increments;
let convertToArray;
let concentric = ["valuesPrimitive", "operatorsPrimitive", "operatorsAdvance"];

function arrayToString(array) {
  for (i = 0; i < array.length; i++) {
    data[0].push([]);
    data[1].push(array[i]);
  }
  return data;
}
function convertToID(name) {
  let id = "#" + name;
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

function setCirclePoints(radius, steps, centerX, centerY) {
  xValues = [];
  yValues = [];
  for (let i = 0; i <= steps; i++) {
    xValues.push(
      Math.round(centerX + radius * Math.cos(2 * Math.PI * (i / steps))) + "px"
    );
    yValues.push(
      Math.round(centerY + radius * Math.sin(2 * Math.PI * (i / steps))) + "px"
    );
  }
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
  setCirclePoints(radius, radialDivisions, centerCoor.x, centerCoor.y);
  let indexGetter = data[1].findIndex((item) => item === event);
  increments = { x: xValues, y: yValues };
  data[0][indexGetter].push(increments);
  increments = [];
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
  let positions = arrayToString(concentric);
  for (i = 0; i < positions[1].length; i++) {
    convertToArray = defineRadials(positions[1][i]);
    h = 0;
    for (let child of defineRadials(positions[1][i]).forEach) {
      h++;
      child.style = `
      position: absolute;
      left:${data[0][i][0].x[h]};
      top: ${data[0][i][0].y[h]};
      `;
    }
  }
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
      <button
        class="rounded-full bg-slate-200 aspect-square"
        id="centerButton"
        @click="positionRails()"
      >
        =
      </button>
    </div>
  </div>
</template>

<style scoped>
* {
  padding: 0 ;
  margin: 0;
  box-sizing: border-box;
}
#centerButton {
  position: fixed;
  left: 50%;
  top: 60%;
  transform: translate(-50%, -50%);
}
#headDiv {
  width: 20vw;
  aspect-ratio: 1;
  position: fixed;
  top: 25%;
  left: 50%;
  transform: translate(-50%, -50%);
}
#bodyDiv {
  width: 30vw;
  aspect-ratio: 1;
  position: fixed;
  left: 50%;
  top: 60%;
  transform: translate(-50%, -50%);
}
</style>
