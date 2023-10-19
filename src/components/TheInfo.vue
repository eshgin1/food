<template>
    <div class="info" id="info">
        <div class="info-about">
            <div class="info-title">О нас</div>
            <div class="info-subtitle">Компания Insight Food занимается организацией правильного питания с доставкой его на дом. Главная цель сервиса — приготовление вкусной и полезной пищи с расчетом рациона на целый день. Комплексные завтраки, обеды и ужины формируют меню, подходящее для здорового образа жизни. <br><br> Наша еда подходит как худеющим людям, профессиональным спортсменам, так и людям стремящимся поддерживать хорошую форму.</div>
        </div>
        <div class="info-order">
            <div class="info-title">Заказ</div>
            <div class="info-subtitle">Наш менеджер подберет вам правильную программу питания</div>
            <a href="#program" class="btn info-btn">Оформить заказ</a>
            <div class="info-subtitle">Хотите мы вам перезвоним?</div>
            <div class="info-subtitle blue">Да, заказать обратный звонок</div>
        </div>
        <div class="info-callback">
            <div class="info-title">ЕСТЬ ВОПРОСЫ?</div>
            <div class="info-subtitle">Обращайтесь! Мы всегда на связи и проконсультируем вам по любым интересующим вас вопросам. Вы можете связаться с нами любым удобным вам способом либо оставив заявку на <span class="info-subtitle blue">обратный звонок</span> - мы вам обязательно перезвоним.</div>
            <form class="form">
                <div class="form-item">
                    <div class="form-title">Ваше имя:</div>
                    <input type="text" class="input info-input" v-model="name" minlength="5" name="name">
                </div>
                <div class="form-item">
                    <div class="form-title">Контактный телефон:</div>
                    <input type="tel" class="input info-input" v-model="phone" name="phone">
                </div>
                <div class="form-item">
                    <div class="form-title">Сообщение:</div>
                    <input type="text" class="input info-input" v-model="message" name="message">
                </div>
                <button class="btn" @click="onSumbitInTelegram">{{ btnText }}</button>
            </form>
            <div class="modal info-modal" v-show="showModal">
                <form class="modal-content">
                    <h1 class="modal-text">Благодарим за обращение! В ближайшее время наш менеджер свяжется с Вами</h1>
                    <div class="modal-close" @click="showModal = false"></div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    import { ref } from 'vue'
    export default{
        setup(){
            const TELEGRAM_BOT_TOKEN = '6448515073:AAHQZ4XNZkpHuhzq9viCotRee8iok0Re-40'
            const TELEGRAM_CHAT_ID = '@InsightFood'
            const API = `https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`
            const name = ref('')
            const phone = ref('+7')
            const message = ref('')
            let btnText = ref('Отправить')
            const showModal= ref(false)
            // const minLength = ref(3)

            // const closeModal = () => {
            //     showModal.value = false
            // }

            async function onSumbitInTelegram (event) {
                event.preventDefault()

                // if(name.value.length > 3 && phone.value.length > 2 && message.value != ''){
                //     const text = `Сообщение с сайта: \n ${message.value}\n от: ${name.value},\n номер телефона: ${phone.value}`
                //     try {
                //         btnText.value = 'Loading...'
                //         const response = await fetch(API, {
                //         method: 'POST',
                //             headers: {
                //                 'Content-Type': 'application/json;charset=utf-8'
                //             },
                //             body: JSON.stringify({
                //                 chat_id: TELEGRAM_CHAT_ID,
                //                 text,
                //             })
                //         });
                //         if(response.ok){
                //             name.value = ''
                //             phone.value = '+7'
                //             message.value = '',
                //             showModal.value = true
                //         }else{
                //             console.log('+')
                //         }
                //     } catch (error) {
                //         console.log(error)
                //     } finally{
                //         btnText.value = 'Отправить'
                //     }
                // }else{
                //     console.log('-')
                // }




                const text = `Сообщение с сайта: \n ${message.value}\n от: ${name.value},\n номер телефона: ${phone.value}`
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
                        name.value = ''
                        phone.value = '+7'
                        message.value = '',
                        showModal.value = true
                    }else{
                        console.log('+')
                    }
                } catch (error) {
                    console.log('-')
                } finally{
                    btnText.value = 'Отправить'
                }
               
            }
            return{
                name,
                phone,
                message,
                btnText,
                showModal,

                onSumbitInTelegram
            }
        }
    }
</script>

<style>
    .info{
        padding: 30px 0;
        display: grid;
        grid-template-columns: 1fr 420px;
        gap: 40px;
    }
    .info-title{
        margin-bottom: 30px;
        font-size: 44px;
        font-weight: 700;
    }
    .info-subtitle{
        font-size: 16px;
    }
    .info-subtitle.blue{
        font-size: 20px;
        color: blue;
    }
    .info-about{
        padding: 20px;
    }
    .info-order{
        padding: 20px;
        background-color: #F2F2F2;
        border-radius: 20px;
    }
    .info-btn{
        margin-top: 20px;
        margin-bottom: 20px;
        font-size: 20px;
    }
    .info-callback{
        padding: 20px;
        grid-column-start: 1;
        grid-column-end: 3;
    }
    .form{
        margin-top: 20px;
        display: grid;
        grid-template-columns: 180px 180px 1fr 180px;
        align-items: end;
        gap: 30px;
    }
    .info-input{
        width: 100%;
    }
    .info-modal{
        padding: 45px;
    }
</style>