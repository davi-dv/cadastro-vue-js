<template>
    <div id="cliente" :class="{'cliente':!isPremium,'cliente-premium':isPremium}">
       <h4>Nome:{{cliente.nome}}</h4>
       <hr>
       <p>Email:{{cliente.email| processarEmail}}</p>
        <hr>
       <p v-if="showIdade===true">Idade:{{cliente.idade}}</p>
       <p v-else-if="showIdade===false">O usuario escondeu a idade!!</p>
       
       <button class="button is-info is-light" @click="mudarCor($event)" >Mudar cor</button>
       <button class="button is-danger" @click="emitirEventoDelete()">Deletar</button>
       <H4>id especial:{{idEspecial}}</H4>
      
    </div>
</template>

<script>
export default {
    data(){
        return{
            isPremium:false
        }
    },
    props:{
        cliente:Object,
        showIdade:Boolean
    },
    methods:{
        mudarCor($event){
            this.isPremium=!this.isPremium;
            console.log($event)
        },
        emitirEventoDelete(){
            console.log('emitindo do filho');
            this.$emit("meDelete",{id_cliente:this.cliente.id,curso:"formação node-js",promocao:true,component:this})

        },
        testar(){
            console.log('testando')
            alert('isso é um alert')
        }
    },
    filters:{
        processarEmail(value){
            return "guia do programador" + value.toUpperCase();
        }
    },
    computed:{
        idEspecial(){
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
   
}
</script>

<style scoped>
.cliente{
    background-color: rgb(31, 180, 196);
    max-width: 600px;
    height: 300px;
    padding: 1%;
    margin: auto;
    margin-top: 2%;
    text-align: center;
}
.cliente-premium{
    background-color: black;
    color:yellow;
    max-width: 600px;
    height: 250px;
    padding: 1%;
    margin-top: 2%;
}

</style>