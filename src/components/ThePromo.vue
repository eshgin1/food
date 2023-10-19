<template>
    <div class="promo">
        <div class="slider">
            <div class="wrapper" :style="{'margin-left': -(100 * currentIndex)+'%'}">
                <div class="slider-img slider-img-1">
                    <div class="slider-info">
                        <h1 class="slider-title">Правильное питание</h1>
                        <h2 class="slider-subtitle">При приготовлении нашей еды используются только свежие продукты.</h2>
                        <h2 class="slider-subtitle">Еда занимает важное место в жизни каждого человека, наша компания отказалась от замороженных продуктов, сделав выбор в пользу свежих.</h2>
                        <h1 class="slider-title slider-title-small">Ежедневная доставка рационов ПП по Сочи, Адлеру, Дагомысу</h1>
                    </div>
                </div>
                <div class="slider-img slider-img-2">
                    <div class="slider-info">
                        <h1 class="slider-title">Худеть вкусно</h1>
                        <h2 class="slider-subtitle">Все программы отличаются большим ассортиментом блюд, чьи вкус и качество остаются на высоте.</h2>
                    </div>
                </div>
            </div>
            <div class="btn btn-prev" @click="prev">
                <div class="arrow prev"></div>
            </div>
            <div class="btn btn-next" @click="next">
                <div class="arrow next"></div>
            </div>
        </div>
        <div class="promo-wrapper">
            <div class="promo-item">
                <img src="../assets/img/watermelon.png" alt="pic" class="promo-img">
                <div class="promo-text">Только свежие продукты</div>
            </div>
            <div class="promo-item">
                <img src="../assets/img/delivery.png" alt="pic" class="promo-img">
                <div class="promo-text">Доставка всегда во время</div>
            </div>
            <div class="promo-item">
                <img src="../assets/img/cook.png" alt="pic" class="promo-img">
                <div class="promo-text">Профессиональные повара</div>
            </div>
            <div class="promo-item">
                <img src="../assets/img/garant.png" alt="pic" class="promo-img">
                <div class="promo-text">Гарантия результата</div>
            </div>
            <div class="promo-item">
                <img src="../assets/img/eat.png" alt="pic" class="promo-img">
                <div class="promo-text">Питательный и вкусный рацион</div>
            </div>
        </div>
    </div>
</template>

<script>
    import { ref } from 'vue'
    export default{
        components:{
            
        },
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
        margin: 0 auto;
        max-width: 1100px;
        overflow: hidden;
    }
    .slider-img{
        display: flex;
        align-items: center;
        min-width: 1100px;
        height: 400px;
        background: url('../assets/img/slider-01.jpg') center/cover no-repeat;
        border-radius: 20px;
    }
    .slider-info{
        margin-left: 70px;
        width: 500px;
    }
    .slider-img-1{
        background: url('../assets/img/slider-01.jpg') center/cover no-repeat;
    }
    .slider-img-2{
        background: url('../assets/img/slider-02.jpg') center/cover no-repeat;
    }
    .slider-title{
        font-size: 44px;
        font-weight: 700;
    }
    .slider-title-small{
        margin-top: 20px;
        font-size: 30px;
    }
    .slider-subtitle{
        margin-top: 10px;
        font-size: 16px;
        font-weight: 400;
    }
    .wrapper{
        display: flex;
        transition: 0.3s;
    }
    /* .img{
        min-width: 1100px;
        height: 200px;
    } */
    .red{
        background: red;
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
    .promo-wrapper{
        margin-top: 50px;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        gap: 30px;
    }
    .promo-text{
        margin-top: 10px;
        font-size: 16px;
    }
    .promo-item{
        display: flex;
        flex-direction: column;
        width: 165px;
        text-align: center;
    }
    .promo-img{
        display: block;
        margin: 0 auto;
        width: 50px;
    }
</style>