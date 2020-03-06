<template>
  <div class="home">
    <div class="container-fluid">
    <h1> bem vindo a {{title}} </h1>

    <h3 v-if="horas >=7 && horas <17" id="aberta" >ABERTA </h3>
    <h3 v-else-if="horas >=17 && horas <18" id="proxima-fechar" >PROXIMA A FECHAR </h3>
    <h3 v-else id="fechada" >FECHADA</h3>
    

  <ul class="col-3" >
  <li v-bind:key="filme.id" v-for="filme in filmes" >{{filme.titulo}}</li>
  
</ul>
  <div class="row">
     <div class="col">
       <h2>Filmes encontrados</h2>
     </div>
   </div>
 
   <div class="row">
 
     <div class="col-md-3"  v-bind:key="filme.id" v-for="filme in filmes">
       <div class="card">
         <img v-bind:src="filme.imagem" class="card-img-top" alt="imagem do filme">
         <div class="card-body">
           <h5 class="card-title">{{ filme.titulo }}</h5>
           <p class="card-text">{{ filme.descricao }}</p>
           <p class="card-text">{{ filme.valor | formatarPreco("R$") }}</p>
           <a href="#" @click="adicionarAoCarrinho(filme)" class="btn btn-primary">Alugar</a>
         </div>
       </div>
     </div>
 
   </div>
    

    </div>
</div>
    

</template>

<script>
export default {
 name: "Home",
 data: function() {
   return {
    
     title: "Locadora de Filmes",
     horas: new Date().getHours(),
     filmes: [
       { id: 1, titulo: "Vingadores", descricao: "Um filme de heróis", valor: 25, imagem: "https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMEDMzGG1lkpnENo3hRNA6TSyZqWuGKc2GR0qg6z3j8Ca3AYlx" },
       { id: 2, titulo: "Pantera Negra", descricao: "Um filme de panteras", valor: 35, imagem: "https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMEDMzGG1lkpnENo3hRNA6TSyZqWuGKc2GR0qg6z3j8Ca3AYlx" },
       { id: 3, titulo: "Homem-Formiga", descricao: "Um filme de formigas", valor: 20, imagem: "https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMEDMzGG1lkpnENo3hRNA6TSyZqWuGKc2GR0qg6z3j8Ca3AYlx" },
       { id: 4, titulo: "Capitã Marvel", descricao: "Um filme de capitãs", valor: 40, imagem: "https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMEDMzGG1lkpnENo3hRNA6TSyZqWuGKc2GR0qg6z3j8Ca3AYlx" },
       { id: 5, titulo: "Hulk", descricao: "Um filme de força", valor: 10, imagem: "https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcTMEDMzGG1lkpnENo3hRNA6TSyZqWuGKc2GR0qg6z3j8Ca3AYlx" }
     ],
     carrinho:[],
     }
   }, methods: {
       adicionarAoCarrinho: function(filme){
         this.carrinho.push(filme.id);
       },
       computed:{
         quantidadeNoCarrinho: function(){
           return this.carrinho.length;
         }
       }
  }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#aberta{
  color: blue;
}
#proxima-fechar{
  color:orange;
}
#fechada{
  color :red;
}

</style>
