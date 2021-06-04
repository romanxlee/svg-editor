<template>
  <div class="container">
    <div class="buttons-container">
        <div class="button" @click="circleCreate">ADD CIRCLE</div>
        <div class="button" @click="rectangleCreate">ADD RECTANGLE</div>
        <div class="button" @click="triangleCreate">ADD TRIANGLE</div>
        <div class="button" @click="starCreate">ADD STAR</div>
    </div>

    <canvas :id="canvasId" class="canvas-style">
    </canvas>

    <div class="log">
      <div class="log__item" v-for="item in figures" :key="item.id">
        <p class="log__text">
          ID: {{item.id}},
        </p>
        <p class="log__text">
          Создан в: {{item.date}},
        </p>
        <p class="log__text">
          Тип: {{item.description}}
        </p>
        <div class="button button_remove" @click="removeFigure(item, item.id)"></div>
      </div>
    </div>
  </div>
</template>

<script>
    const paper = require('paper');
    export default {
      components: {
      },
        props: ['canvasId'],
        data: () => ({
            path: null,
            scope: null,
            figures: []
        }),
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
              const myRectangle = new paper.Rectangle(new paper.Point(450, 350), new paper.Point(150, 100))
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
            /* mouseMove() {
              let self = this;
              this.tool = this.createTool(this.scope);
              this.tool.onMouseDrag = (event) => {
                self.path = this.newCircle
                self.path.selected = true
                self.path.position = event.point
              }
              this.tool.onMouseUp = () => {
                self.path.selected = false
              }
            } */
        },
        mounted() {
            this.scope = new paper.PaperScope();
            this.scope.setup(this.canvasId);
            this.circleCreate(this.scope)
        }
    }
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  gap: 10px;
}
    .canvas-style {
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

    .button_remove {
      background-image: url(../assets/delete.svg);
      background-size: cover;
      background-repeat: no-repeat;
      width: 15px;
      height: 15px;
      border: none;
    }

    .log {
      width: 15%;
      max-height: 500px;
      border: 1px solid black;
      overflow-y: auto;
    }

    .log__item {
      display: flex;
      flex-direction: column;
      gap: 5px;
      align-items: center;
      padding: 5px 0;
      outline: 1px solid black;
    }

    .log__text {
      margin: 0;
    }
</style>