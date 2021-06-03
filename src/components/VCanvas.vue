<template>
    <div>
        <canvas :id="canvasId" class="canvas-style">
        </canvas>
        <div class="button" @click="addCircle">ADD CIRCLE</div>
        <div class="button" @click="addRectangle">ADD RECTANGLE</div>
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
        }),
        methods: {
            circleCreate() {
                const myCircle = new paper.Path.Circle(new paper.Point(100, 70), 50);
                myCircle.fillColor = 'black'
                myCircle.onMouseDrag = (event) => {
                myCircle.selected = true
                myCircle.position = event.point
              }
                myCircle.onMouseUp = () => {
                  myCircle.selected = false
                }
                return myCircle
            },
            rectangleCreate() {
              const myRectangle = new paper.Rectangle(new paper.Point(450, 350), new paper.Point(150, 100))
              const myPath = new paper.Path.Rectangle(myRectangle)
              myPath.fillColor = 'black'
                myPath.onMouseDrag = (event) => {
                myPath.selected = true
                myPath.position = event.point
              }
              myPath.onMouseUp = () => {
                  myPath.selected = false
                }
              return myPath
            },
            addCircle() {
              this.circleCreate()
            },
            addRectangle() {
              this.rectangleCreate()
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
            this.rectangleCreate(this.scope)
        }
    }
</script>

<style scoped>
    .canvas-style {
        cursor: pointer;
        width: 100% !important;
        height: 500px !important;
        border: 5px solid black;
        border-radius: 10px;
        display: block;
        margin: auto;
        box-shadow: 0 10px 8px -8px black;
    }
    .button {
      border: 1px solid black;
      cursor: pointer;
    }
</style>