<template>
    <div class="advantages">
        <div class="advantages-title">ПРЕИМУЩЕСТВА ПРАВИЛЬНОГО ПИТАНИЯ</div>
        <div class="advantages-block">
            <ul class="advantages-list">
                <li class="advantages-item" v-for="(item, i) in advantagesArr" :key="'id'+i">
                    <img :src="item.icon" alt="icon" class="advantages-icon">
                    <div class="advantages-text">{{ item.text }}</div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import body from '../assets/img/body.png'
    import heart from '../assets/img/heart.png'
    import shoes from '../assets/img/shoes.png'
    import smail from '../assets/img/smail.png'
    export default{
        components:{
        },
        setup(){
            const advantagesArr = [
                {text: 'Улучшение внешности', icon: body},
                {text: 'Нормализация настроения', icon: smail},
                {text: 'Дополнительная энергия', icon: shoes},
                {text: 'Снижение рисков', icon: heart}
            ]
            return{
                advantagesArr
            }
        }
    }
</script>

<style scoped>
    .advantages{
        margin-top: 50px;
    }
    .advantages-title{
        font-size: 44px;
        font-weight: 700;
        color: #93278F
    }
    .advantages-item{
        margin-top:20px;
        display: flex;
    }
    .advantages-block{
        margin-top: 20px;
        padding: 50px;
        border-radius: 20px;
        background: url('../assets/img/polyana.jpg') center center/cover no-repeat;
    }
    .advantages-text{
        margin-left: 10px;
        font-size: 24px;
        font-weight: 300;
    }
</style>