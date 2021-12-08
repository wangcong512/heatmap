<template>
    <div id="heatmap" ref="heatmap"></div>

</template>

<script>
    import heatmapLib from 'heatmap.js'
    export default {
        name: "HeatMap",
        data:function () {
            return {}
        },
        mounted() {
            this.init()
        },
        methods:{
            init(){

                this.initHeatMap()
            },
            initHeatMap() {

                let heatmap = heatmapLib.create({
                    container: this.$refs['heatmap'], //容器
                });
                heatmap.setData({
                    max: 5,
                    data: [{ x: 10, y: 15, value: 5}, { x: 100, y: 15, value: 3.5},
                        { x: 30, y: 30, value: 50},
                        { x: 40, y: 55, value: 50},
                        { x: 50, y: 75, value: 50}
                        ]
                })


                let width = this.$refs['heatmap'].clientWidth;
                let height = this.$refs['heatmap'].clientHeight;

                let generate = function() {


                    let x = (Math.random()* width) >> 0;
                    let y = (Math.random()* height) >> 0;
                    let c = 100;
                    let r = (Math.random()* 100) >> 0;

                    // add the datapoint to heatmap instance
                    heatmap.addData({ x: x, y:y, value: c, radius: r});
                };

                // this generates new datapoints in a kind of random timing
                let count = 0
                setTimeout(function test() {
                    let rand = (Math.random() * 100) >> 0;
                    generate();
                    count++
                    if(count < 100) {
                        setTimeout(test, rand);
                    }
                }, 10);

            }

        }
    }
</script>

<style lang="scss" scoped>
    #heatmap{
        position: absolute;
        top: 0;
        width: 800px;
        height: 600px;
        background-color: #2c3e50;
        margin: auto;
    }

</style>
