            <!--  Aula 256 - Como criar e usar componentes 
                  Aula 260 - Props 
                  Aula 261 Diretivas condicionais V-if 
                  Aula 263 V-for 
                  Aula 265 Formulários 
                  Aula 266 Validaçõa 
                  Aula 267 Emissão de Eventos 
                  Aula 270 Computed e como instalar bibliotecas vue  -->

/<!--(1-256)-->
<template>
  <div id = "app">

    <div class="buttons">
      <button class="button is-primary">Button</button>
      <button class="button is-link">Button</button>
    </div>

<!--(9-265) Criando um formulário-->
    <h3>Formulário de Cadastro: </h3>
    <input type="text" placeholder="nome" v-model="nomeField"><br>
    <input type="email" placeholder="email" v-model="emailField"><br>
    <input type="number" placeholder="idade" v-model="idadeField">
<!--Vai disparar um evento (Chamando o método (cadastrar usuário 11-265))-->
    <button @click="cadastrarUsuario">Cadastrar</button>
    <hr>



    <h1>Guia Clientes App.vue</h1>
    <Produto/> <!--AQR Produto.vue-->
<!--(5-260)-->
    <input type="text" v-model="clienteAmanda.nome">
    <input type="text" v-model="clienteAmanda.email">
<!--(6-261) Vou Chamar a prop ShowIdade (ARQ Cliente.vue 7-261)-->
    <Cliente :cliente="clienteAmanda" :showIdade="true"/>
    <Cliente :cliente="clienteAmanda" :showIdade="false"/>

    <hr>
    <hr>


    <h1>V-For App.vue</h1>
  <!--(8-263) Vou criar um diretiva V-for, para cada cliente, dentro da VARIÁVEL clientes, eu vou ter uma
  key, para identificar um cliente do outro'-->

  <!--(17-270) Em vez de exibir um array de clientes não ordenado eu vou exibir ele de forma odernada
  substituindo (Clientes) por (orderClientes)-->
    <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <h4>{{ index + 1 }}</h4> <!--Chamando a variável index para listar o posicionamento-->
      <!-- O componente cliente recebe uma prop chamada cliente (5-260) que recebe a variável cliente-->
  
      <!--(13-267) Chamando o evento customizado (meDelete ARQ App.vue 16-267) (deletarusuario 14-267) -->
      <!--Com o $event Estou puxando essas informações curso: "Formação Node.js", emPromocao: true-->
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>
      
      <hr>
    <h3>Edição: </h3>
    <input type="text" v-model="cliente.nome">
    <input type="text" v-model="cliente.email">
    </div>
  </div>  
</template>


<!--(2-256) Importando componentes-->
<script>
// Importando arquivo Cliente.vue
import Cliente from './components/Cliente'
import Produto from './components/Produto.vue'

// (15-270) Importando Biblioteca lodash
import _ from 'lodash';

export default {
  name: 'App',
/*(4-260) Vou chamar a função data (ARQ Cliente.vue 4-260) */
  data(){
    return{
      clienteAmanda: {
        nome: "Amanda Lima",
        email: "amanda@lima",
        idade: 26
      },
/*(7-263) Vou criar um dado chamado clientes que vai ser um array (VAI TER 3 CLIENTES) para cada cliente eu vou 
gerar um elemento HTML  */
      clientes: [
        
        {
        id: 3,
        nome: "Patrick Gomes",
        email: "patrick@lima",
        idade: 15
        },
        {
        id: 4,
        nome: "Bob Esponja",
        email: "bob@lima",
        idade: 18
        },
      ],
/*(10-265) Criando 3 variáveis */
        nomeField: "",
        emailField: "",
        idadeField: 0,
    }
  },

/*(3-256) Vou criar uma variável components e importar o arquivo Cliente */
  components: {
    Cliente,
    Produto
  },
/*(11-265) Vou adicionar o objeto de métodos (Cadastrar usuários) */
  methods: {
    cadastrarUsuario: function(){
/*(12-266) Vou criar uma validação para o formulário */
// Se nomefiled é uma strinf vazia, ou com espações ou menor que 3 caracteres vou printar um erro no console
      if(this.nomeField == "" || this.nomeField == " " || this.nomeField < 3){
        alert("Erro de Validação");
// Se nenhuma das minhas condições forem verdades eu vou cadastrar no meu else
      }else{
      // Vou chamar o array de cliente (7-263), Push -> é um método que serve para adicionar dados em array
      this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()})
      // Assim que cadastrar vai limpar os campos para mim
      this.nomeField ="";
      this.emailField = "";
      this.idadeField = 0;
      }
    },

/*(14-267) Vou criar um método Deletar Usuário */
    deletarUsuario: function($event){
      console.log("Recebendo Evento");
      console.log($event)
      console.log($event.idDoCliente)
      var id = $event.idDoCliente;
  // Filtro é uma função que recebe uma regra dentro do parenteses, onde para cada cliente dentro array vai aplicar
  // essa regra e vai retornar um novo array 
  // REGRA: "Para cada cliente ele compare se o id do cliente é diferente da minha variável, se o id do cliente "
  // Se o id do cliente é diferente que eu estou recebendo, ele vai manter esse cliente dentro do array, se o 
  // id do cliente é igual ao que eu quero remover, ele vai remover
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      // A lista de Cliente recebe um novo array
      this.clientes = novoArray
    }
  },

/*(16-270) Criar uma Computed Properties */
  computed: {
    orderClientes: function(){
      // Vou rodar a ordenação de função do lodash (ESSA REGRA ABAIXO ESTÁ NA DOCUMENTAÇÃO DO LODASH)
      // Estou ordenando o array de clientes de forma crescente 
      return _.orderBy(this.clientes, ['nome'], ['asc']);
    }
  }

}
</script>

<style>

</style>

