<template>
  <div id="app">
    <h3>Cadastro:</h3>
    <small id="nome-erro" v-show="deu_erro">O nome é inválido,tente novamente!</small>
    <br />

    <input type="text" placeholder="nome" v-model="nomeField" />
    <br />
    <input type="text" placeholder="email" v-model="emailField" />
    <br />
    <input type="number" placeholder="idade" v-model="idadeField" />
    <br />
    <button id="btn-cadastrar" class="button is-success" @click="cadastraCliente()">Cadastrar</button>
    <hr />
    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h1>{{index}}</h1>
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)" />
    </div>
  </div>
</template>


<script>
import Cliente from "./components/Cliente";
import _ from "lodash";

export default {
  name: "App",
  data() {
    return {
      deu_erro: false,
      nomeField: "",
      emailField: "",
      idadeField: "",

      clientes: [
        {
          id: 1,
          nome: "Davi o programador junior",
          email: "davi@teste",
          idade: 32,
        },
        {
          id: 2,
          nome: "joao batista",
          email: "joao@teste",
          idade: 32,
        },
      ],
    };
  },

  components: {
    Cliente,
  },

  methods: {
    cadastraCliente() {
      if (
        this.nomeField.trim() === "" ||
        this.emailField.trim() === "" ||
        this.idadeField.trim() === ""
      ) {
        this.deu_erro = true;
      } else {
        this.clientes.push({
          nome: this.nomeField,
          email: this.emailField,
          idade: this.idadeField,
          id: Date.now(),
        });
        this.emailField = "";
        this.nomeField = "";
        this.idadeField = "";
        console.log(this.clientes);
      }
    },
    deletarUsuario($event) {
      console.log($event);
      let id = $event.id_cliente;
      let novoArray = this.clientes.filter((cliente) => cliente.id != id);
      this.clientes = novoArray;
    }
  },
  computed: {
    orderClientes() {
      return _.orderBy(this.clientes, ["nome", ["asc"]]);
    }
  },
};
</script>


<style>
#nome-erro {
  color: red;
}
#app{
  text-align: center;
  padding-top: 5%;
}
#btn-cadastrar{
 margin-top: 10px;
}
</style>
