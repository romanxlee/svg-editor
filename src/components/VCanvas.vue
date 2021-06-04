<template>
  <div class="container">
    <div class="buttons-container">
        <div class="button" @click="circleCreate">Добавить Круг</div>
        <div class="button" @click="rectangleCreate">Добавить Прямоугольник</div>
        <div class="button" @click="triangleCreate">Добавить Треугольник</div>
        <div class="button" @click="starCreate">Добавить Звезду</div>
    </div>

    <canvas :id="canvasId" class="canvas">
    </canvas>

    <Log
      :data="figures"
      @buttonClick="removeFigure"
    />
  </div>
</template>

<script>
import Log from '@/components/Log';
const paper = require('paper');

export default {
  props: ['canvasId'],
  data: () => ({
    scope: null,
    figures: [],
  }),
  components: {
    Log
  },
  methods: {
    circleCreate() {
        const myCircle = new paper.Path.Circle(new paper.Point(100, 70), 50);
        myCircle.fillColor = 'black'
        myCircle.onMouseDrag = (event) => this.mouseDrag(myCircle, event)
        myCircle.onMouseUp = () => this.mouseUp(myCircle)
        myCircle.description = 'Круг'
        myCircle.date = new Date().toLocaleString('ru', {hour: 'numeric', minute: 'numeric', second: 'numeric'})
        this.figures.push(myCircle)
        return myCircle
    },
    rectangleCreate() {
      const myRectangle = new paper.Rectangle(new paper.Point(250, 150), new paper.Point(150, 100))
      const myPath = new paper.Path.Rectangle(myRectangle)
      myPath.fillColor = 'blue'
      myPath.onMouseDrag = (event) => this.mouseDrag(myPath, event)
      myPath.onMouseUp = () => this.mouseUp(myPath)
      myPath.description = 'Прямоугольник'
      myPath.date = new Date().toLocaleString('ru', {hour: 'numeric', minute: 'numeric', second: 'numeric'})
      this.figures.push(myPath)
      return myPath
    },
    triangleCreate() {
      const myTriangle = new paper.Path.RegularPolygon(new paper.Point(80, 70), 3, 50)
      myTriangle.fillColor = 'yellow'
      myTriangle.onMouseDrag = (event) => this.mouseDrag(myTriangle, event)
      myTriangle.onMouseUp = () => this.mouseUp(myTriangle)
      myTriangle.description = 'Треугольник'
      myTriangle.date = new Date().toLocaleString('ru', {hour: 'numeric', minute: 'numeric', second: 'numeric'})
      this.figures.push(myTriangle)
      return myTriangle
    },
    starCreate() {
      const newStar = new paper.Path.Star({
        center: [50, 50],
        points: 5,
        radius1: 20,
        radius2: 50,
        fillColor: 'red',
      })
      newStar.rotate(35)
      newStar.onMouseDrag = (event) => this.mouseDrag(newStar, event)
      newStar.onMouseUp = () => this.mouseUp(newStar)
      newStar.description = 'Звезда'
      newStar.date = new Date().toLocaleString('ru', {hour: 'numeric', minute: 'numeric', second: 'numeric'})
      this.figures.push(newStar)
      return newStar
    },
    mouseDrag(el, event) {
      el.selected = true;
      el.position = event.point
    },
    mouseUp(el) {
      el.selected = false
    },
    removeFigure(item, id) {
      item.remove()
      this.figures = this.figures.filter(item => item.id !== id)
    }
  },
  mounted() {
      this.scope = new paper.PaperScope();
      this.scope.setup(this.canvasId);
      this.circleCreate(this.scope)
  }
}
</script>

<style>
.container {
  width: 100%;
  display: flex;
  gap: 10px;
}

.canvas {
    cursor: pointer;
    width: 80% !important;
    height: 500px !important;
    border: 5px solid black;
    border-radius: 10px;
    display: block;
}

.button {
  border: 1px solid black;
  cursor: pointer;
}
</style>
