<template>
    <footer class="footer">
        <div class="footer-wrapper">
            <div class="footer-block">
                <div class="footer-text">2022 Insight Food (C) Все права защищены. <br>Перепечатка или копирование материалов сайта запрещено</div>
                <div class="footer-text">Краснодарский Край, г. Сочи</div>
                <a href="tel:+79528278833" class="footer-text">+7(952)827-88-33</a>
            </div>
            <div class="footer-block">
                <div class="footer-btns">
                    <button class="btn btn-black">Обратный звонок</button>
                    <a href="#program" class="btn">Сделать заказ</a>
                </div>
                <div class="footer-social">
                    <a href="https://wa.me/79528278833">
                        <img src="../assets/icons/whatsapp.svg" alt="whatsapp">
                    </a>
                    <a href="https://instagram.com/insighte.food">
                        <img src="../assets/icons/instagram.svg" alt="inst">
                    </a>
                </div>
            </div>
        </div>
    </footer>
</template>

<script>
    export default{
    components: { 

    },
    setup(){
        
        return{
            
        }
    }
}
</script>

<style scoped>
    .footer{
        padding: 30px 0;
        background: #F2F2F2;
    }
    .footer-wrapper{
        width: 1200px;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }
    .footer-btns{
        display: flex;
        gap: 20px;
    }
</style>