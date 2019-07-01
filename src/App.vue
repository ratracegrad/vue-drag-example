<template>
    <v-app id="app">
        <!--        <v-container fluid style="border: 1px solid blue;">-->
        <!--            <div-->
        <!--                id="item"-->
        <!--                ref="item"-->
        <!--                @touchstart="dragStart($event)"-->
        <!--                @touchend="dragEnd($event)"-->
        <!--                @touchmove="drag($event)"-->
        <!--                @mousedown="dragStart($event)"-->
        <!--                @mouseup="dragEnd($event)"-->
        <!--                @mousemove="drag($event)"-->
        <!--            >-->
        <!--                <v-icon color="black">drag_handle</v-icon>-->
        <!--                <p>First Item</p>-->
        <!--                <p>Second Item</p>-->
        <!--                <p>Third Item</p>-->
        <!--            </div>-->
        <!--        </v-container>-->
        <div id="outerContainer">
            <div
                id="container"
                @touchstart="dragStart($event)"
                @touchend="dragEnd($event)"
                @touchmove="drag($event)"
                @mousedown="dragStart($event)"
                @mouseup="dragEnd($event)"
                @mousemove="drag($event)"
            >
                <div id="item" ref="item">
                    <p>Hello World</p>
                    <p>Hello World</p>
                    <p>Hello World</p>
                </div>
            </div>
        </div>
    </v-app>
</template>

<script>
export default {
    name: 'app',
    data() {
        return {
            active: false,
            currentX: null,
            currentY: null,
            initialX: null,
            initialY: null,
            xOffset: 0,
            yOffset: 0
        };
    },
    methods: {
        dragStart(e) {
            if (e.type === 'touchstart') {
                this.initialX = e.touches[0].clientX - this.xOffset;
                this.initialY = e.touches[0].clientY - this.yOffset;
            } else {
                this.initialX = e.clientX - this.xOffset;
                this.initialY = e.clientY - this.yOffset;
            }

            if (e.target === this.$refs.item) {
                this.active = true;
            }
        },
        dragEnd() {
            this.initialX = this.currentX;
            this.initialY = this.currentY;

            this.active = false;
        },
        drag(e) {
            if (this.active) {
                e.preventDefault();

                if (e.type === 'touchmove') {
                    this.currentX = e.touches[0].clientX - this.initialX;
                    this.currentY = e.touches[0].clientY - this.initialY;
                } else {
                    this.currentX = e.clientX - this.initialX;
                    this.currentY = e.clientY - this.initialY;
                }

                this.xOffset = this.currentX;
                this.yOffset = this.currentY;

                this.setTranslate(0, this.currentY, this.$refs.item);
            }
        },
        setTranslate(xPos, yPos, el) {
            el.style.transform =
                'translate3d(' + xPos + 'px, ' + yPos + 'px, 0)';
        }
    }
};
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: flex;
    justify-content: center;
    align-items: center;
}
#container {
    width: 100%;
    height: 400px;
    background-color: #333;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 7px;
    touch-action: none;
}
#item {
    width: 100%;
    /*height: 100px;*/
    background-color: rgb(245, 230, 99);
    border: 10px solid rgba(136, 136, 136, 0.5);
    /*border-radius: 50%;*/
    touch-action: none;
    user-select: none;
}
#item:active {
    background-color: rgba(168, 218, 220, 1);
}
#item:hover {
    cursor: pointer;
    /*border-width: 20px;*/
}
/*#item {*/
/*    !*width: 100%;*!*/
/*    touch-action: none;*/
/*    user-select: none;*/
/*    background: white;*/
/*    padding: 20px;*/
/*}*/
/*#item:active {*/
/*    background-color: rgba(168, 218, 220, 1);*/
/*}*/
/*#item:hover {*/
/*    cursor: pointer;*/
/*}*/
p {
    border-bottom: 1px solid black;
    color: black;
}
</style>
