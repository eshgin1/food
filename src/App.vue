<template>
  <TheTop/>
  <div class="container">
    <TheHeader/>
    <ThePromo/>
    <TheProgram/>
    <TheReviews/>
    <TheAdvantages/>
    <TheDelivery/>
    <TheInfo/>
  </div>
  <TheFooter/>
</template>

<script>
  import TheTop from './components/TheTop.vue';
  import TheHeader from './components/TheHeader.vue';
  import ThePromo from './components/ThePromo.vue';
  import TheProgram from './components/TheProgram.vue';
  import TheReviews from './components/TheReviews.vue';
  import TheAdvantages from './components/TheAdvantages.vue';
  import TheDelivery from './components/TheDelivery.vue';
  import TheInfo from './components/TheInfo.vue';
  import TheFooter from './components/TheFooter.vue';

  export default {
    name: 'App',
    components: {
      TheHeader, TheTop, ThePromo, TheProgram, TheAdvantages,
      TheReviews, TheDelivery, TheInfo,
      TheFooter, 
    },
    data(){

      return{
      }
    }
  }
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    text-decoration: none;
    list-style-type: none;
    scroll-behavior: smooth;
  }
  .container{
    width: 1200px;
    margin: 0 auto;
  }
  .btn{
    padding: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    background-color: #39B54A;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .btn:hover{
    opacity: 0.8;
  }
  .btn-black{
    background: #000;
  }
  .input{
    margin-top: 10px;
    padding: 10px 10px;
    border: 1px solid #d8d6de;
    border-radius: 5px;
    background: none;
    font-size: 13px;
    box-shadow: 0 2px 8px 0 rgb(34 41 47/14%)
  }
  .modal{
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
  .modal-text{
    margin-top: 10px;
    font-size: 18px;
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
  }
  .modal-btn{
    margin-top: 15px;
  }
</style>
