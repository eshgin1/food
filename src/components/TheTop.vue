<template>
    <div class="top">
        <div class="top-block">
            <a href="tel:+79528278833" class="phone">+7 (952) 827-88-33</a>
            <button class="btn btn-black" @click="openModalCallback">Обратная связь</button>
            <a href="#program" class="btn">Сделать заказ</a>
        </div>
        <div class="modal" v-show="showModalCallback">
            <form  class="modal-content">
                <div class="modal-title">Обратный звонок</div>
                <div class="modal-input">
                    <div class="modal-subtitle">Ваше имя:</div>
                    <input type="text" name="name" v-model="name" class="input">
                </div>
                <div class="modal-input">
                    <div class="modal-subtitle">Номер телефона:</div>
                    <input type="tel" name="phone" v-model="phone" class="input">
                </div>
                <button type="submit" @click="onSumbitInTelegram" class="btn modal-btn">{{ btnText }}</button>
                <div v-if="thanks" class="modal-text">Спасибо за заявку, мы свяжемся с Вами в близжайщее время</div>
                <div class="modal-close" @click="closeModalCallback"></div>
            </form>
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
            const thanks = ref(false)
            const btnText = ref('Заказать звонок')

            async function onSumbitInTelegram (event) {
                event.preventDefault()


                const text = `Обратная связь \n имя: ${name.value},\n номер телефона: ${phone.value}`
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
                    }else{
                        console.log('=')
                    }
                } catch (error) {
                    console.log('-')
                } finally{
                    btnText.value = 'Заказать звонок'
                    name.value = ''
                    phone.value = '+7'
                }
               
            }
            

            const showModalCallback = ref(false)

            const openModalCallback = () => {
                showModalCallback.value = true
            }
            const closeModalCallback = () => {
                showModalCallback.value = false
                thanks.value = false
            }
            return{
                name,
                phone,
                thanks,
                btnText,

                showModalCallback,
                openModalCallback,
                closeModalCallback,

                onSumbitInTelegram,
            }
        }
    }
</script>

<style>
    .top{
        display: flex;
        justify-content: center;
        align-items: center;
        background: #F2F2F2;
    }
    .top-block{
        padding: 7px;
        width: 1200px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        gap: 20px;
    }
    .phone{
        font-size: 16px;
        color: #000;
    }
</style>