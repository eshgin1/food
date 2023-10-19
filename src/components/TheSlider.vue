<template>
    <div class="slider">
            <slot></slot>
            <!-- <div class="wrapper" :style="{'margin-left': -(100 * currentIndex)+'%'}"> -->
                
                <!-- <div class="img red"></div>
                <div class="img"></div> -->
            <!-- </div> -->
            <div class="btn btn-prev" @click="prev">
                <div class="arrow prev"></div>
            </div>
            <div class="btn btn-next" @click="next">
                <div class="arrow next"></div>
            </div>
        </div>
</template>

<script>
import { ref } from 'vue'
    export default{
        setup(){
            let currentIndex = ref(0)

            const prev = () => {
                if(currentIndex.value > 0){
                    currentIndex.value--
                }
            }
            
            const next = ()=> {
                if(currentIndex.value < 1){
                    currentIndex.value++
                }
            }

            return{
                currentIndex,
                prev,
                next,
            }
        }
    }
</script>

<style scoped>
    .slider{
        position: relative;
        max-width: 1100px;
        overflow: hidden;
    }
    .wrapper{
        display: flex;
        transition: 0.3;
    }

    .btn{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 38px;
        height: 38px;
        border-radius: 50%;
        background-color: rgba(87, 87, 87, 0.082);
        cursor: pointer;
    }
    .btn-prev{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
    }
    .btn-next{
        position: absolute;
        right: 0;
        top: 50%;
        transform: translateY(-50%);
    }
    .arrow{
        border: solid black;
        border-width: 0 3px 3px 0;
        display: inline-block;
        padding: 4px;
    }
    .prev{
        transform: rotate(135deg);
    }
    .next{
        transform: rotate(-45deg);
    }
</style>