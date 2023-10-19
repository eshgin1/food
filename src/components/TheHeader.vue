<template>
    <div class="header">
        <a href="#" class="header-logo">
            <img :src="logo" alt="logo" class="header-img">
        </a>
        <ul class="header-list">
            <a class="header-link" href="">Главная</a>
            <a class="header-link" href="#program">Программы питания</a>
            <a class="header-link" href="#delivery">Доставка</a>
            <a class="header-link" href="#info">О нас</a>
        </ul>
        <div class="header-social">
            <a href="https://wa.me/79528278833" class="social">
                <img src="../assets/icons/whatsapp.svg" alt="telegram" class="icon whatsapp">
            </a>
            <a href="https://instagram.com/insighte.food" class="social">
                <img src="../assets/icons/instagram.svg" alt="inst" class="icon inst">
            </a>
        </div>
    </div>
</template>

<script>
    import logo from '@/assets/img/logo.png'
    export default{
        setup(){
            return{
                logo
            }
        }
    }
</script>

<style scoped>
    .header{
        display: grid;
        align-items: center;
        grid-template-columns: 200px 1fr 1fr;
    }
    .header-img{
        width: 100%;
    }
    .header-list{
        display: flex;
        gap: 20px;
    }
    .header-link{
        padding: 5px;
        font-weight: 700;
        font-size: 17px;
        color: #000;
        cursor: pointer;
        border-radius: 7px;
        transition: 0.2s;
    }
    .header-social{
        display: flex;
        justify-content: flex-end;
    }
    .header-link:hover{
        background: #000;
        color: #fff;
    }
</style>