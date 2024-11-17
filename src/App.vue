<script setup>
  import { ref, onMounted } from "vue"

  const coins = ref([
    { code: 'USD', text: 'United States Dollar'},
    { code: 'MXN', text: 'Peso Mexicano'},
    { code: 'EUR', text: 'Euro'},
    { code: 'GBP', text: 'Pound'},
  ])

  const cryptocurrency = ref([])

  onMounted(() => {
    const url = 'https://min-api.cryptocompare.com/data/top/mktcapfull?limit=20&tsym=USD'

    // Get API
    fetch(url)
      // Get the response in JSON
      .then(response => response.json())
      // Data
      .then(({Data}) => cryptocurrency.value = Data)
  })
</script>

<template>
  <div class="contenedor">
    <h1 class="titulo">
      <span>Cryptocurrency</span>
      Price Calculator
    </h1>

    <div class="contenido">
      <form class="formulario">
        <div class="campo">
          <label for="moneda">Coin:</label>

          <select id="moneda">
            <option value="">--Select--</option>
            <option
              v-for="coin in coins"
              :value="coin.code"
            >{{ coin.text }}</option>
          </select>
        </div>
      </form>
    </div>
  </div>
</template>