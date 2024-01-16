<script setup>
import { reactive } from 'vue';

  const nome = "Rodrigo"
  const meuObj = {
    nome: "Rodrigo",
    filmeFavorito: "Gladiador"
  }

  function dizOla(nome) {
    return `${nome} diz oi`;
  }

  const enderecoImagem = "https://media.gettyimages.com/id/156473199/pt/foto/russell-crowe-with-sword-in-a-scene-from-the-film-gladiator-2000.jpg?s=1024x1024&w=gi&k=20&c=mIxodMMMeLycdMoaK_sJ2lvqdEHv36HhPk0rJZ2A4Ew="
  const ImagemSuperman = "https://www.cnnbrasil.com.br/wp-content/uploads/sites/12/2022/12/221024162135-man-of-steel-cavill.jpg?w=1220&h=674&crop=1"
  const botaoDesabilitado = false

  const gostaDeGladiador = false
  const gostaSuperman = false

  const estaAutorizado = false

  //let contador = 0
  const estado = reactive({
    contador: 0,
    email: '',
    saldo: 5000,
    transferindo: 0,
    nomes: ['gian', 'paula', 'luiza', 'monica'],
    nomeAInserir: ''
  })

  function incrementar() {
    estado.contador++;
  }

  function decrementar() {
    estado.contador--;
  }

  function alterEmail(evento) {
    estado.email = evento.target.value
  }

  function  mostraSaldoFuturo() {
    const {saldo, transferindo} = estado;
    return saldo - transferindo;
  }

  function validaValorTransferencia() {
    const {saldo, transferindo} = estado;
    return saldo >= transferindo;
  }

  function cadastrarNome() {
    if (estado.nomeAInserir.length >=3) {
      estado.nomes.push(estado.nomeAInserir);
    } else {
      alert('Digite mais caracteres');
    }
  }

</script>

<template>
  <h1>{{ dizOla(nome) }}</h1>
  <img v-if="gostaDeGladiador" :src=enderecoImagem alt="">
  <img v-else-if="gostaSuperman" :src="ImagemSuperman" alt="">
  <h2 v-else>Não curte filmes</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoDesabilitado">Enviar mensagem</button>

  <br>
  <hr>

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="email" @keyup="alterEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }} <br>
  Transferindo: {{ estado.transferindo }} <br>
  Saldo depois da transferência: {{ mostraSaldoFuturo()}} <br>
  <input class="campo" :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>

  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nome</button>

</template>

<style scoped>
  img {
    max-width: 200px;
  }

  .invalido {
    outline-color: red;
    border-color: red;
  }

  .campo {
    border: 2px solid #000;
  }
</style>
