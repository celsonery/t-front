<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <label for="proto">Procolo</label>
    <select name="proto" v-model="protocol">
      <option value="http://" selected>http</option>
      <option value="https://">https</option>
    </select>
    <label for="ip">Endereço IP</label>
    <input name="ip" type="text" v-model="ipAddress" />

    <label for="port">Porta</label>
    <input name="port" type="number" v-model="port" />
  </div>

  <div class="card">
<!--    <button type="button" @click="count++">count is {{ count }}</button>-->
    <button type="button" @click="test">Test connection</button>
  </div>

</template>

<script setup>
import {onMounted, ref} from 'vue'
import axios from 'axios'

defineProps({
  msg: String
})

const count = ref(0)
const protocol = ref('http://')
const ipAddress = ref('127.0.0.1')
const port = ref('9200')

onMounted
{
  console.log("Testando onMount no Vue 3")
}

function test() {
  console.log("Methodo test funcionando: " + protocol.value)

  axios.get(protocol.value + ipAddress.value + ":" + port.value)
    .then(res => {
      console.log("Requisição OK: ", res)
    })
    .catch(err => {
      console.log("Erro: ", err)
    })
}
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
}
</style>
