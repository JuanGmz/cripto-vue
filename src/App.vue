<script setup>
  import { ref, reactive, onMounted } from "vue"

  const coins = ref([
    { code: 'USD', text: 'United States Dollar'},
    { code: 'MXN', text: 'Peso Mexicano'},
    { code: 'EUR', text: 'Euro'},
    { code: 'GBP', text: 'Pound'},
  ])

  const cryptos = ref([])
  const calculate = reactive({
    coin: '',
    crypto: ''
  })

  onMounted(() => {
    const url = 'https://min-api.cryptocompare.com/data/top/mktcapfull?limit=20&tsym=USD'

    // Get API
    fetch(url)
      // Get the response in JSON
      .then(response => response.json())
      // Data
      .then(({Data}) => cryptos.value = Data)
  })
</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">
      <span>Cryptos</span>
      Price Calculator
    </h1>

    <div class="contenido">
      <form class="formulario">
        <div class="campo">
          <label for="coin">Coin:</label>

          <select 
            id="coin"
            v-model="calculate.coin"  
          >
            <option value="">--Select--</option>
            <option
              v-for="coin in coins"
              :value="coin.code"
            >{{ coin.text }}</option>
          </select>
        </div>

        <div class="campo">
          <label for="crypto">Crypto:</label>

          <select 
            id="crypto"
            v-model="calculate.crypto"
          >
            <option value="">--Select--</option>
            <option
              v-for="crypto in cryptos"
              :value="crypto.CoinInfo.Name"
            >{{ crypto.CoinInfo.FullName }}</option>
          </select>
        </div>

        <input type="submit" value="Calculate">
      </form>
    </div>
  </div>
</template>