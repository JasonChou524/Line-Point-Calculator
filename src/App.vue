<script setup>
import { ref } from 'vue'

const total = ref(null)
const giveBack = ref(null)
const usePoint = ref(0)
const needPay = ref(0)
const getPoint = ref(0)
const showMonitor = ref(false)

const clickConfirm = () => {
  usePoint.value =
    total.value -
    Math.ceil(
      (Math.round(total.value * (giveBack.value / 100)) - 0.5) /
        (giveBack.value / 100)
    )

  needPay.value = Math.ceil(
    (Math.round((total.value * giveBack.value) / 100) - 0.5) /
      (giveBack.value / 100)
  )

  getPoint.value = Math.round(total.value * (giveBack.value / 100))

  showMonitor.value = true
}

const clickClear = () => {
  total.value = null
  giveBack.value = null
  showMonitor.value = false
}
</script>

<template>
  <div class="container">
    <h1>點數計算機</h1>
    <div class="card">
      <div class="monitor">
        <ul v-show="showMonitor">
          <li>花費點數：{{ usePoint }} 點</li>
          <li>支付金額：{{ needPay }} 元</li>
          <li>獲得點數：{{ getPoint }} 點</li>
        </ul>
      </div>
      <input v-model="total" type="number" placeholder="請輸入金額" />
      <input v-model="giveBack" type="number" placeholder="請輸入回饋趴數(%)" />
      <div class="btn">
        <button @click="clickConfirm" class="confirm">確認</button>
        <button @click="clickClear" class="clear">清除</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  background-color: #a8d3fe;
  height: 100vh;
  max-height: -webkit-fill-available;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  h1 {
    font-weight: 400;
    margin-bottom: 10px;
  }
}
.card {
  box-sizing: border-box;
  width: 300px;
  height: 350px;
  padding-top: 40px;
  background-color: #fff;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 72px;
  display: flex;
  flex-direction: column;
  align-items: center;

  input {
    box-sizing: border-box;
    width: 224px;
    height: 39px;
    padding: 5px;
    margin-bottom: 10px;
    border: 1px solid #afafaf;
    border-radius: 5px;
    font-size: 20px;
    &::placeholder {
      color: #888;
    }
  }
}

.monitor {
  box-sizing: border-box;
  width: 244px;
  height: 122px;
  margin-bottom: 20px;
  padding-left: 20px;
  padding-top: 12px;
  background-color: #d9d9d9;
  border: #000 solid 2px;
  border-radius: 20px;
  ul {
    display: inline-block;
    // display: none;
    list-style-type: none;
    font-size: 20px;
    font-weight: 400;
    li {
      margin-bottom: 5px;
    }
  }
}

.btn {
  margin-top: 10px;
  button {
    width: 80px;
    height: 35px;
    border: 0px;
    border-radius: 25px;
    color: black;
    font-size: 20px;
    &:active {
      box-shadow: 0 2px rgb(68, 60, 60);
      transform: translateY(2px);
    }
  }
  .confirm {
    background-color: #56bffa;
    margin-right: 15px;
    box-shadow: 0 4px #1f698e;
  }
  .clear {
    background-color: #fa5656;
    box-shadow: 0 4px #7e2b2b;
  }
}
</style>
