<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'

const getAPI = `https://v6.exchangerate-api.com/v6/${import.meta.env.VITE_API_KEY}/latest/USD`

const amount = ref(0)
const fromCurrency = ref('TWD')
const toCurrency = ref('USD')
const rates = ref({})
const result = ref(0)
const updateTime = ref('')

function calculate(){
  result.value = (amount.value / rates.value[fromCurrency.value] * rates.value[toCurrency.value]).toFixed(2)
}

async function apiData() {
  try{
    const response = await axios.get(getAPI)
    rates.value = response.data.conversion_rates
    const date = new Date(response.data.time_last_update_unix * 1000)
    updateTime.value = `${date.getFullYear()}/${String(date.getMonth() + 1).padStart(2, '0')}/${String(date.getDate()).padStart(2, '0')}`
  }catch(error){
    console.error(error)
  }
}

onMounted(apiData)
</script>

<template>
  <div class='allPages'>
    <div class='card'>
      <p class='card-title'>
        匯率換算器
      </p>
      <p class='card-subtitle'>
        即時匯率，每日更新
      </p>

      <p class='input-label'>
        輸入金額
      </p>
      <div class='dollarInput'>
        <input
          v-model='amount'
          type='text'
        >
      </div>

      <p class='input-label'>
        選擇幣別
      </p>
      <div class='currency-value'>
        <select v-model='fromCurrency'>
          <option
            v-for='(rate, currency) in rates'
            :key='currency'
            :value='currency'
          >
            {{ currency }}
          </option>
        </select>
        <span class='arrow'>→</span>
        <select v-model='toCurrency'>
          <option
            v-for='(rate, currency) in rates'
            :key='currency'
            :value='currency'
          >
            {{ currency }}
          </option>
        </select>
      </div>

      <button
        class='btn'
        @click='calculate'
      >
        換算
      </button>

      <div class='result'>
        <p class='result-label'>
          換算結果
        </p>
        <p class='result-value'>
          {{ result }}
        </p>
        <p class='result-unit'>
          {{ toCurrency }}
        </p>
      </div>

      <p class='update-time'>
        匯率更新時間：{{ updateTime }}
      </p>
    </div>
  </div>
</template>

<style>
  body {
    margin: 0;
    padding: 0;
  }
</style>

<style scoped>

.allPages {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  min-height: 100vh;
  background-color: #2b2b2b;
  padding: 16px;
  box-sizing: border-box;
}

.card {
  background-color: #3a3a3a;
  border-radius: 12px;
  border: 1px solid #4a4a4a;
  padding: 2rem;
  width: 100%;
  max-width: 400px;
  box-sizing: border-box;
}

.card-title {
  font-size: 22px;
  font-weight: 500;
  color: #ffffff;
  margin-bottom: 4px;
}

.card-subtitle {
  font-size: 13px;
  color: #aaaaaa;
  margin-bottom: 1.25rem;
}

.input-label {
  font-size: 13px;
  color: #aaaaaa;
  margin-bottom: 6px;
  margin-top: 14px;
}

.dollarInput input {
  width: 100%;
  height: 44px;
  padding: 0 14px;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #4a4a4a;
  box-sizing: border-box;
  color: #ffffff;
  background-color: #2b2b2b;
}

.currency-value {
  display: flex;
  align-items: center;
  gap: 10px;
}

.currency-value select {
  flex: 1;
  height: 44px;
  border-radius: 8px;
  border: 1px solid #4a4a4a;
  padding-left: 10px;
  color: #ffffff;
  background-color: #2b2b2b;
}

.arrow {
  color: #888888;
  font-size: 18px;
}

.btn {
  margin-top: 20px;
  width: 100%;
  height: 44px;
  border-radius: 8px;
  border: 1px solid #4a4a4a;
  background-color: #3a3a3a;
  color: #ffffff;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
}

.result {
  margin-top: 14px;
  border-radius: 8px;
  background-color: #2b2b2b;
  text-align: center;
}

.result-label {
  padding-top: 24px;
  margin-bottom: 8px;
  color: #aaaaaa;
  font-size: 13px;
}

.result-value {
  font-size: 36px;
  font-weight: 500;
  color: #4da6ff;
}

.result-unit {
  margin-top: 8px;
  padding-bottom: 24px;
  font-size: 14px;
  color: #aaaaaa;
}

.update-time {
  margin-top: 14px;
  font-size: 11px;
  color: #666666;
  text-align: center;
}

</style>
