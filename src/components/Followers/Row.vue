<template>
    <div class="progress">
        <div class="bar" :style="styles">{{count}}</div>
    </div>
</template>
<script>
    import TWEEN from '@tweenjs/tween.js';
    export default {
        props: {
            row: {
                type: Object,
                require: true,
            },
            animate: {
                type: Boolean,
                required: true,
            },
            duration: {
                type: Number,
                required: true,
            }
        },
        data(){
            return{
                minWidth: 10,
                tweeningValue: 0,
            }
        },
        computed: {
            styles() {
                let style = 'width:' + this.tweeningValue + '%;'
                if(!this.row.gradient)
                    style += 'background-color:'+this.row.color;
                else
                    style += 'background-image: linear-gradient('+ this.row.color.join(', ') +')';
                return style
            },
            count() {
                return this.row.count > 999 ? (this.row.count / 1000).toFixed(1) + 'k' : this.row.count;
            }
        },
        watch: {
            animate: function(newValue) {
                if(newValue){
                    let num = this.row.percent < this.minWidth ? this.minWidth : this.row.percent
                    this.tween(0, num)
                }
            }
        },
        methods: {
            tween: function (startValue, endValue) {
            var vm = this
            function animate () {
                if (TWEEN.update()) {
                    requestAnimationFrame(animate)
                }
            }

            new TWEEN.Tween({ tweeningValue: startValue })
                .to({ tweeningValue: endValue }, 500)
                .onUpdate(function (object) {
                vm.tweeningValue = object.tweeningValue.toFixed(0)
                })
                .start()

            animate()
            }
        }
    }
</script>

<style scoped>

.progress {
    float: right;
    width: 70%;
}
.bar {
    height: 30px;
    border-radius: 10px;
    color: white;
    font-weight: bold;
    font-size: 12px;
    text-align: center;
}
</style>