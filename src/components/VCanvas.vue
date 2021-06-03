<template>
    <div>
        <canvas :id="canvasId" class="canvas-style" v-on:mousemove="onMouseMove"
        />
    </div>
</template>

<script>
    const paper = require('paper');
    export default {
        props: ['canvasId'],
        data: () => ({
            path: null,
            scope: null
        }),
        methods: {
            circleCreate(scope) {
                scope.activate();
                const myCircle = new paper.Path.Circle(new paper.Point(100, 70), 50);
                myCircle.fillColor = 'black'
                return myCircle
            },
            rectangleCreate(scope) {
              scope.activate();
              const myRectangle = new paper.Rectangle(new paper.Point(450, 350), new paper.Point(150, 100))
              const myPath = new paper.Path.Rectangle(myRectangle)
              myPath.fillColor = 'black'
              myPath.selected = true
              return myPath
            },
            onMouseMove(event) {
              this.myCircle.position = event.point;
            }
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
        cursor: crosshair;
        width: 100% !important;
        height: 500px !important;
        border: 5px solid black;
        border-radius: 10px;
        display: block;
        margin: auto;
        box-shadow: 0 10px 8px -8px black;
    }
</style>