<template>
  <div>
    <h1>Welcome {{ nome }}</h1>
    <input type="text" :value="nome" @input="mudouTexto"/>
    <input type="password" v-model="senha"/>
    <p v-if="nome.length > 10">Nome longo!</p>
    <p v-else>Nome curto!</p>
    <button @click="buscarUsuarios">Atualizar</button>
    <CustomTable :usuarios="usuarios"/>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import CustomTable from '@/components/CustomTable.vue';
import axios from 'axios';

const nome = ref("teste");
const senha = ref("senha");
const usuarios = ref([ {id:1, nome: "Geraldo"}, {id: 2, nome: "Cláudia"}]);

async function buscarUsuarios() {
  usuarios.value = (await axios.get('usuario')).data;
}

function mudouTexto(e: any) {
  nome.value = e.target.value;
}

</script>