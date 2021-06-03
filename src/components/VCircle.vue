<template>
    <div>
        <canvas :id="canvasId" class="canvas-style" v-on:mousedown="mouseMove"
        />
    </div>
</template>

<script>
    const paper = require('paper');
    export default {
        props: ['canvasId'],
        data: () => ({
            path: null,
            scope: null,
            newCircle: null
        }),
        methods: {
            circleCreate(scope) {
                scope.activate();
                const myCircle = new paper.Path.Circle(new paper.Point(100, 70), 50);
                myCircle.fillColor = 'black'
                return this.newCircle =  myCircle
            },
            /* rectangleCreate(scope) {
              scope.activate();
              const myRectangle = new paper.Rectangle(new paper.Point(450, 350), new paper.Point(150, 100))
              const myPath = new paper.Path.Rectangle(myRectangle)
              myPath.fillColor = 'black'
              return myPath
            }, */
            createTool(scope) {
              scope.activate();
              return new paper.Tool();
            },
            mouseMove() {
              let self = this;
              this.tool = this.createTool(this.scope);
              this.tool.onMouseDrag = (event) => {
                self.path = this.newCircle
                self.path.position = event.point
              }
            }
        },
        mounted() {
            this.scope = new paper.PaperScope();
            this.scope.setup(this.canvasId);
            this.circleCreate(this.scope)
            //this.rectangleCreate(this.scope)
        }
    }
</script>

<style scoped>
    .canvas-style {
        width: 100px;
        height: 200px;
        cursor: pointer;
        border: 5px solid black;
        border-radius: 10px;
        display: block;
        margin: auto;
        box-shadow: 0 10px 8px -8px black;
    }
</style>