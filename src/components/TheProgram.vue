<template>
    <div class="program" id="program">
        <h1 class="program-title">программы питания</h1>
        <div class="tabs">
            <ul class="tabs-header">
                <li class="tabs-weigth" :class="{active: activeTab === item.id}"
                    v-for="(item) in tabsArr"
                    :key="item.id"
                    @click="openNextTab(item)"   >
                    {{ item.calories }}</li>
            </ul>
            <div class="tabs-content" >
                <div class="tabs-block" v-for="(item, i) in tabsArr" :key="item.id" v-show="activeTab === i">
                    <div>
                        <div class="tabs-item">
                            <div class="tabs-title">{{ item.title}}</div>
                            <div class="tabs-text tabs-calories">{{ item.calories}}</div>
                            <div class="tabs-text tabs-medium">Средний БЖУ <span class="span span-green">{{ item.medium }}</span></div>
                        </div>
                        <div class="tabs-item">
                            <div class="tabs-title">Пример 1 дня меню:</div>
                            <div class="tabs-text tabs-menu">завтрак: {{ item.breakfast }}</div>
                            <div class="tabs-text tabs-menu" v-if="item.secondBreakfast">второй завтрак: {{ item.secondBreakfast }}</div>
                            <div class="tabs-text tabs-menu">обед: {{ item.lunch}}</div>
                            <div class="tabs-text tabs-menu" v-if="item.secondLunch">полдник: {{ item.secondLunch}}</div>
                            <div class="tabs-text tabs-menu">ужин: {{ item.dinner }}</div>
                            <div class="tabs-text tabs-menu" v-if="item.secondDinner">второй ужин: {{ item.secondDinner }}</div>
                        </div>
                        <div class="tabs-item" v-for="(price, ind) in item.price" :key="'id'+ind">
                            <div class="tabs-text tabs-price">1 день <span class="span">{{price.one}}</span> рублей</div>
                            <div class="tabs-text tabs-price">5 дней {{ price.five }} рублей/день <span class="span">{{ price.fiveTotal}}</span> рублей</div>
                            <div class="tabs-text tabs-price">7 дней {{ price.seven }} рублей/день <span class="span">{{ price.sevenTotal }}</span> рублей</div>
                            <div class="tabs-text tabs-price">14 дней {{ price.fourteen }} рублей/день <span class="span">{{ price.fourteenTotal }}</span> рублей</div>
                            <div class="tabs-text tabs-price">30 дней {{price.thirty}} рублей/день <span class="span">{{ price.thirtyTotal }}</span> рублей</div>
                        </div>

                        <MyButton @click="openModal">Оформить подписку</MyButton>

                        <div class="modal" v-show="showModal">
                            <form class="modal-content">
                                <div class="modal-title">Сделать заказ</div>
                                <div class="modal-subtitle">Оформить подписку на программу {{ item.calories }}</div>
                                <div class="modal-input">
                                    <div class="modal-subtitle">Ваше имя:</div>
                                    <input type="text" v-model="name" name="name" class="input">
                                </div>
                                <div class="modal-input">
                                    <div class="modal-subtitle">Номер телефона:</div>
                                    <input type="tel" v-model="phone" name="phone" class="input">
                                </div>
                                <button @click="onSumbitInTelegram(item.calories)" class="btn modal-btn">{{btnText}}</button>
                                <div class="modal-text" v-if="thanks">Спасибо за заказ</div>
                                <div class="modal-close" @click="closeModal"></div>
                            </form>
                        </div>
                    </div>
                    <div class="tabs-pic">
                        <img :src="item.img" alt="pic" class="tabs-img">
                    </div>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
    import { ref } from 'vue';
    import MyButton from './UI/MyButton.vue';
    import ration from '../assets/img/ration.jpg'
    import ration1 from '../assets/img/ration1.jpg'
    import ration2 from '../assets/img/ration2.jpg'
    import ration3 from '../assets/img/ration3.jpg'
    import ration4 from '../assets/img/ration4.jpg'

    export default{
        components:{
            MyButton
        },
        setup(){
            // const src = ration
            const TELEGRAM_BOT_TOKEN = '6448515073:AAHQZ4XNZkpHuhzq9viCotRee8iok0Re-40'
            const TELEGRAM_CHAT_ID = '@InsightFood'
            const API = `https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`
            const name = ref('')
            const phone = ref('+7')
            const thanks = ref(false)
            const btnText = ref('Оформить заказ')

            let activeTab = ref(0);

            let showModal = ref(false)

            const openModal = () => {
                showModal.value = true
            }

            const closeModal = () => {
                showModal.value = false
                thanks.value = false
            }

            const tabsArr = ref([
                {id: 0, calories: '800-900 ккал', title: 'Снижение веса', medium:'52/32/70', breakfast: 'Мексиканская кесадилья с цыплёнком',lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили', dinner: 'Салат «Цезарь с курицей»', price: [{one: '1150', five: '1100', fiveTotal: '5500', seven: '1050',  sevenTotal: '7370', fourteen: '950', fourteenTotal: '13300', thirty: '900', thirtyTotal: '2700'}], img: ration},
                {id: 1, calories: '1100-1200 ккал', title: 'Снижение веса', medium:'80/55/85', breakfast: 'Мексиканская кесадилья с цыплёнком', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной' ,lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили', dinner: 'Салат «Цезарь с курицей»',  price: [{one: '1300', five: '1250', fiveTotal: '6250', seven: '1200',  sevenTotal: '8400', fourteen: '1100', fourteenTotal: '14000', thirty: '1050', thirtyTotal: '31500'}], img: ration1},
                {id: 2, calories: '1400-1500 ккал', title: 'Снижение веса', medium:'100/55/105', breakfast: 'Мексиканская кесадилья с цыплёнком', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной', lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили', secondLunch: 'Форель с овощами по-нормандски', dinner: 'Салат «Цезарь с курицей»',  price: [{one: '1150' , five: '1500', fiveTotal: '5500', seven: '1150', sevenTotal: '5500', fourteen: '1150', fourteenTotal: '5500', thirty: '1150', thirtyTotal: '5500'}], img: ration1},
                {id: 3, calories: '1600-1700 ккал', title: 'Баланс', medium:'120/75/130', breakfast: 'Мексиканская кесадилья с цыплёнком', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной', lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили, Тыквенный крем-суп с креветкой', secondLunch: 'Форель с овощами по-нормандски', dinner: 'Салат «Цезарь с курицей»',  price: [{one: '1650', five: '1600 ', fiveTotal: '8000 ', seven: '1550',  sevenTotal: '10850', fourteen: '1500', fourteenTotal: '21000', thirty: '1450', thirtyTotal: '43500'}], img: ration2},
                {id: 4, calories: '1800-1900 ккал', title: 'Баланс', medium:'130/80/145', breakfast: 'Кукурузная каша на кокосовом молоке с курагой', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной', lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили, Крем-суп из тыквы с креветками', secondLunch: 'Форель с овощами по-нормандски', dinner: 'Салат «Цезарь с курицей»',  price: [{one: '1800', five: '1750', fiveTotal: '8750', seven: '1700',  sevenTotal: '11900', fourteen: '1650', fourteenTotal: '23100', thirty: '1550', thirtyTotal: '46500'}], img: ration2},
                {id: 5, calories: '2000-2200 ккал', title: 'Набор', medium:'150/90/170', breakfast: 'Кукурузная каша на кокосовом молоке с курагой', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной' ,lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили', secondLunch: 'Мексиканская кесадилья с цыплёнком', dinner: 'Форель с овощами по-нормандски', secondDinner: 'Салат «Цезарь с курицей»', price: [{one: '1900', five: '1850', fiveTotal: '9250', seven: '1700',  sevenTotal: '12600', fourteen: '1750', fourteenTotal: '24500', thirty: '1650', thirtyTotal: '49500'}], img: ration3},
                {id: 6, calories: '2400-2500 ккал', title: 'Набор', medium:'165/105/220', breakfast: 'Кукурузная каша на кокосовом молоке с курагой', secondBreakfast: 'Корзиночки на рисовой муке с творожным кремом и малиной' ,lunch: 'Пряный рис с с куриной грудкой, овощным миксом и сладким Чили, Крем-суп из тыквы с креветкой', secondLunch: 'Мексиканская кесадилья с цыплёнком', dinner: 'Форель с овощами по-нормандски', secondDinner: 'Салат «Цезарь с курицей»',  price: [{one: '2100', five: '2050', fiveTotal: '10250', seven: '2000',  sevenTotal: '14000', fourteen: '1950', fourteenTotal: '27300', thirty: '1850', thirtyTotal: '55500'}], img: ration3},
                {id: 7, calories: '1000-1200 ккал', title: 'Кето-диета', medium:'65/80/25', breakfast: 'Цветные спагетти из овощей с креветками в сливках', secondLunch: 'Мексиканская кесадилья с цыплёнком',  dinner: 'Салат с форелью слабой соли',  price: [{one: '2100', five: '2050', fiveTotal: '1300', seven: '1250',  sevenTotal: '6250', fourteen: '1200', fourteenTotal: '8400', thirty: '1100', thirtyTotal: '15400'}], img: ration4},
            ])

            const openNextTab = (item) => {
                activeTab.value = item.id
            }
            
            async function onSumbitInTelegram (calories){
                event.preventDefault()
                
                let text = `Новый заказ\n ${calories}\n ${name.value}\n ${phone.value}`

                try {
                    btnText.value = 'Loading...'

                    const response = await fetch(API, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json;charset=utf-8'
                        },
                        body: JSON.stringify({
                            chat_id: TELEGRAM_CHAT_ID,
                            text,
                        })
                    });
                    if(response.ok){
                        thanks.value = true
                        name.value = ''
                        phone.value = '+7'
                    }
                    
                } catch (error) {
                    console.log('-')
                } finally{
                    btnText.value = 'Оформить заказ'
                }
            }

            return{
                name,
                phone,
                thanks,
                btnText,

                tabsArr,
                activeTab,
                showModal,
                openNextTab,
                openModal,
                closeModal,
                onSumbitInTelegram
            }
        }
    }
</script>

<style>
    .program{
        margin-top: 50px;
    }
    .program-title{
        font-weight: 700;
        font-size: 44px;
        color: #F7931E;
    }
    .tabs{
        margin-top: 30px;
    }
    .tabs-header{
        display: grid;
        grid-template-columns: repeat(8, 1fr);
    }
    .tabs-weigth{
        display: flex;
        align-items: center;
        justify-content: center;
        height: 56px;
        font-size: 16px;
        padding: 5px;
        border-radius: 18px 18px 0 0;
        cursor: pointer;
    }
    .tabs-weigth.active{
        background:#F2F2F2;
    }
    .tabs-content{
        padding: 24px;
        border: 4px solid #F2F2F2;
    }
    .tabs-block{
        display: grid;
        grid-template-columns: 600px 1fr;
    }
    .tabs-title{
        font-size: 30px;
    }
    .tabs-item{
        margin-top: 20px;
    }
    .tabs-pic{
        display: flex;
        justify-content: center;
    }
    .tabs-text{
        margin-top: 7px;
        font-size: 16px;
    }
    .tabs-img{
        max-width: 500px;
        max-height: 500px;
        border-radius: 10px;
    }
    .span{
        padding: 5px;
        border-radius: 10px;
        background: #000;
        color: #fff;
    }
    .span-green{
        background-color: #27bd93ee;
    }
    /* .modal{
        position: fixed;
        width: 100%;
        height: 100vh;
        background: rgb(16 16 16 / 77%);;
        top: 0;
        left: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 99999;
    }
    .modal-title{
        font-size: 26px;
        text-align: center;
    }
    .modal-subtitle{
        margin-top: 15px;
    }
    .modal-content{
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
        border-radius: 10px;
        background: #fff;
    }

    .modal-close{
        position: absolute;
        top: -20px;
        right: -20px;
        width: 24px;
        height: 24px;
        cursor: pointer;
        transition: opacity ease 0.5s;
    }

    .modal-close::before,
    .modal-close::after {
        content: '';
        position: absolute;
        top: 10px;
        display: block;
        width: 24px;
        height: 3px;
        background: #fff;
    }

    .modal-close::before {
        transform: rotate(45deg);
    }

    .modal-close::after {
        transform: rotate(-45deg);
    } */

</style>