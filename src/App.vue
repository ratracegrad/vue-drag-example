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
                <v-container fluid fill-height id="item" ref="item">
                    <v-layout row wrap class="scroll-box-grid px-2">
                        <v-flex
                            v-for="(machine, $machineIndex) in machines"
                            :key="$machineIndex"
                            class="line-grid-wrap"
                        >
                            <span class="subheading" style="height: 30px;">{{
                                machine.name
                            }}</span>
                        </v-flex>
                    </v-layout>
                </v-container>
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
            yOffset: 0,
            machines: [
                {
                    name: 'Brushless Drill',
                    status: 'up',
                    data: [
                        {
                            workOrderId: '123',
                            sku: '04081962',
                            status: 'green',
                            maintenance: true,
                            offset: 2,
                            length: 8
                        },
                        {
                            workOrderId: '222',
                            sku: '04081962',
                            status: 'red',
                            offset: 24,
                            length: 12
                        }
                    ]
                },
                {
                    name: 'Sample Machine',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 16
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 25,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Hair Dryer',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 5
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 7,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'grey',
                            offset: 12,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Blue Yeti Microphone',
                    status: 'up',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 2,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'red',
                            offset: 6,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Lucky the Cat',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 4
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 13,
                            length: 2
                        },
                        {
                            workOrderId: 'id42',
                            sku: '04081962',
                            status: 'red',
                            offset: 18,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Nalgene Bottle',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 20
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 27,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Brushless Drill',
                    status: 'up',
                    data: [
                        {
                            workOrderId: '123',
                            sku: '04081962',
                            status: 'green',
                            maintenance: true,
                            offset: 2,
                            length: 8
                        },
                        {
                            workOrderId: '222',
                            sku: '04081962',
                            status: 'red',
                            offset: 24,
                            length: 12
                        }
                    ]
                },
                {
                    name: 'Sample Machine',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 16
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 25,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Hair Dryer',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 5
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 7,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'grey',
                            offset: 12,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Blue Yeti Microphone',
                    status: 'up',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 2,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'red',
                            offset: 6,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Lucky the Cat',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 4
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 13,
                            length: 2
                        },
                        {
                            workOrderId: 'id42',
                            sku: '04081962',
                            status: 'red',
                            offset: 18,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Nalgene Bottle',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 20
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 27,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Brushless Drill',
                    status: 'up',
                    data: [
                        {
                            workOrderId: '123',
                            sku: '04081962',
                            status: 'green',
                            maintenance: true,
                            offset: 2,
                            length: 8
                        },
                        {
                            workOrderId: '222',
                            sku: '04081962',
                            status: 'red',
                            offset: 24,
                            length: 12
                        }
                    ]
                },
                {
                    name: 'Sample Machine',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 16
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 25,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Hair Dryer',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 5
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 7,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'grey',
                            offset: 12,
                            length: 8
                        }
                    ]
                },
                {
                    name: 'Blue Yeti Microphone',
                    status: 'up',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 2,
                            length: 2
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'red',
                            offset: 6,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Lucky the Cat',
                    status: 'down',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 0,
                            length: 3
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 5,
                            length: 4
                        },
                        {
                            workOrderId: 'A472',
                            sku: '04081962',
                            status: 'grey',
                            offset: 13,
                            length: 2
                        },
                        {
                            workOrderId: 'id42',
                            sku: '04081962',
                            status: 'red',
                            offset: 18,
                            length: 3
                        }
                    ]
                },
                {
                    name: 'Nalgene Bottle',
                    status: 'maintenance',
                    data: [
                        {
                            workOrderId: 123,
                            sku: '04081962',
                            status: 'green',
                            offset: 1,
                            length: 20
                        },
                        {
                            workOrderId: 222,
                            sku: '04081962',
                            status: 'green',
                            offset: 27,
                            length: 3
                        }
                    ]
                }
            ]
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
}
#container {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 60vh;
    background-color: #333;
    touch-action: none;
}
#item {
    touch-action: none;
    user-select: none;
    position: absolute;
    bottom: 0;
    border: 1px solid red;
}
#item:hover {
    cursor: pointer;
}
.scroll-box-grid {
    height: 100%;
    overflow: auto;
}
.line-grid-wrap {
    cursor: pointer;
    overflow: hidden;
    width: 100%;
    border: 2px solid;
    color: white;
    padding: 5px 0;
    margin: 0 0 10px;
}
</style>
