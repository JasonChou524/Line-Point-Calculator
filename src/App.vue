<script setup>
  import { computed } from "@vue/reactivity";
  import {ref} from "vue"
  
  const rewardPoint = 0.01
  const total = ref()
  const usePoint = computed(() => {
    return (total.value - Math.ceil((Math.round(total.value * rewardPoint) - 0.5) / rewardPoint))
  })
  const needPay = computed(() => {
    return (Math.ceil((Math.round(total.value * rewardPoint) - 0.5) / rewardPoint))
  })
  const getPonit = computed(() => {
    return (Math.round(total.value * rewardPoint))
  })
</script>

<template>
 <div class="container">
  <div class="wrapper">
    <h1>點數計算機</h1>
    <input v-model="total" type="number" placeholder="請輸入金額">
    <ul v-show="total >= 50">
      <li>花費點數：{{ usePoint }} 點</li>
      <li>支付金額：{{ needPay }} 元</li>
      <li>獲得點數：{{ getPonit }} 點</li>
    </ul>
  </div>
 </div>
</template>

<style lang="scss" scoped>
  .container {
    background-color: #A8D3FE;
    height: 100vh;
    max-height: -webkit-fill-available; 
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .wrapper{
    box-sizing: border-box;
    width:  300px;
    height: 350px;
    padding: 60px 40px;
    background-color: #fff;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 72px;
    display: flex;
    flex-direction: column;
    align-items: center;
    h1 {
      font-weight: 400;
      margin-bottom: 10px;
    }
    input {
      box-sizing: border-box;
      width: 150px;
      height: 30px;
      padding: 5px;
      margin-bottom: 10px;
    }
    ul {
      list-style-type: none;
      li {
        margin-bottom: 5px;
      }
    }
  }
</style>
