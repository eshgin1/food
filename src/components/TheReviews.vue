<template>
    <div class="reviews">
        <div class="reviews-title">НАШИ КЛИЕНТЫ О НАС</div>
        <div class="slider">
            <div class="wrapper" :style="{'margin-left': -(30 * count) +'%'}">
                <div class="reviews-item" v-for="(client, i) in reviewsArr" :key="'id'+ i">
                    <div class="reviews-img">
                        <img :src="client.img" alt="photo" class="reviews-photo">
                    </div>
                    <div class="reviews-comment">
                        <div class="reviews-name">{{ client.name}}</div>
                        <div class="reviews-text">{{ client.text}}</div>
                    </div>
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
</template>

<script>
    import { ref } from 'vue'

    import olga from '@/assets/img/person/olga.png'
    import alina from '@/assets/img/person/alina.png'
    import evgenia from '@/assets/img/person/evgenia.png'
    import sofa from '@/assets/img/person/sofa.png'
    import karina from '@/assets/img/person/karina.png'
    import igor from '@/assets/img/person/igor.png'
    export default{
        
        setup(){
            let count = ref(0)
            const prev = () => {
                if(count.value > 0){
                    count.value = count.value - 1
                }
            }
            const next = () => {
                if(count.value < 3){
                    count.value = count.value + 1
                }
            }
            const reviewsArr = [
                {name: 'Евгения', text: 'Инсайт - это про любовь, про здоровье и про счастливый образ жизни.', img: evgenia},
                {name: 'София', text: 'Я всегда беру вашу еду с собой на работу и вообще не думаю о том, что мне кушать! С вами очень удобно:-))', img: sofa},
                {name: 'Алина', text: 'Я обожаю Инсайт! Благодаря нему я забыла о готовке! У меня появилось много времени на свою работу, развитие и семью. Люблю вас!', img: alina},
                {name: 'Карина', text: 'Я обожая ваши ужины! Все так разнообразно и вкусно, что я никогда от вас не уйду))', img: karina},
                {name: 'Игорь', text: 'У меня нет хлопот по готовке еды для работы. Я невероятно разнообразил питание. И да, я стабильно 85кг. Все, как я люблю.', img: igor},
                {name: 'Ольга', text: 'Привет вам и благодарности от всего нашего семейства!:-)', img: olga},
            ]
            return{
                prev,
                next, 
                count,
                reviewsArr
            }
        }
    }
</script>

<style scoped>
    .reviews{
        position: relative;
        margin-top: 50px;
    }
    .reviews-title{
        margin-bottom: 20px;
        font-size: 44px;
        font-weight: 700;
        color: #39B54A;
    }
    .reviews-item{
        display: flex;
        gap: 20px;
        width: 350px;
    }
    .reviews-photo{
        width: 90px;
        height: 90px;
        border-radius: 50%;
    }
    .reviews-comment{
        padding: 5px 13px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        background-color: #F2F2F2;
        border-radius: 20px;
        font-size: 15px;
        line-height: 20px;
        width: 300px;
    }
    .slider{
        position: relative;
        max-width: 1200px;
        overflow: hidden;
    }
    .wrapper{
        display: flex;
        gap: 30px;
        transition: .5s;
    }
    .btn{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 32px;
        height: 32px;
        border-radius: 50%;
        background-color: rgba(87, 87, 87, 0.834);
        cursor: pointer;
    }
    .btn-prev{
        position: absolute;
        top: 70%;
        left: -50px;
        transform: translateY(-50%);
    }
    .btn-next{
        position: absolute;
        right: 0;
        top: 70%;
        right: -50px;
        transform: translateY(-50%);
    }
    .arrow{
        border: solid rgb(255, 255, 255);
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