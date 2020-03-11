<template>
  <div class="home">
    <b-row v-if="mostrarFilmes">
      <h1>Bem vinda a {{ title }}</h1>
    </b-row>
    <!--<b-row>
      <h3 v-if="horas >= 7 && horas < 17" id="aberta">ABERTA</h3>
      <h3 v-else-if="horas >= 17 && horas < 18" id="proxima-fechar">PRÓXIMA DE FECHAR</h3>
      <h3 v-else id="fechada">FECHADA</h3>
    </b-row>-->
    <b-row>
       <button type="button" class="btn btn-dark"     v-on:click="mostrarCarrinho">
         Carrinho: {{ quantidadeNoCarrinho }} filmes
       </button>
    </b-row>

<b-row>
       <button type="button" class="btn btn-warning"     v-on:click="filtra5estrelas">
         Filtra 5 estrelas
       </button>
    </b-row>
    <b-row >
      <div class="cards">
        <b-card  :key="filme.id" v-for="filme in filmesOrdenados"
          :title="filme.titulo"
          :id="filme.id"
          :img-src="filme.imagem"
          img-alt="Image"
          img-top
          tag="article"
          style="width: 14rem"
          class="mb-2"
        >
          <b-card-text>
            {{ filme.descricao }}    
          </b-card-text>
        

          <b-card-text>
            {{ filme.valor | formatarPreco("R$") }}    
          </b-card-text>
          
          <b-card-text> 
            <span v-for="n in 5" :key="n">
              <b-icon icon="star-fill" variant="warning" font-scale="1" v-if="filme.avaliacao >= n"></b-icon> 
              <b-icon icon="star" font-scale="1" variant="warning" v-else></b-icon>
            </span>
          </b-card-text>

          <!--<b-button variant="danger" @click="removeFilmeLista(filme.id)">Remover</b-button>-->
          <b-button href="#" @click="adicionarAoCarrinho(filme)"   v-if="validarPermissaoParaAdicionarNoCarrinho(filme)" variant="dark">Alugar</b-button>

          <b-button href="#"  v-else variant="dark" disabled> Alugar</b-button>
        </b-card>
      </div>
    </b-row>
   
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: { },
  data: function() {
   return {
     mostrarFilmes: true,
     carrinho: [],
     title: "Locadora de Filmes",
     horas: new Date().getHours(),
     filmes_obj: [
       { id: 1, titulo: "Vingadores",avaliacao: 4, descricao: "Um filme de heróis", valor: 25, imagem: "https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27179657%27&EntityType=%27Item%27&EntityId=%2710807%27&Width=720&Height=1080&device=web_browser&subions=Anonymous",   estoqueDisponivel: 3 
       },
       { id: 2, titulo: "Pantera Negra",avaliacao: 2, descricao: "Um filme de panteras", valor: 35,   estoqueDisponivel: 3,imagem: "https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27182460%27&EntityType=%27Item%27&EntityId=%2710148%27&Width=720&Height=1080&device=web_browser&subions=Anonymous" },
       { id: 3, titulo: "Homem-Formiga",avaliacao: 5,   estoqueDisponivel: 3,descricao: "Um filme de formigas", valor: 20, imagem: "https://images-na.ssl-images-amazon.com/images/I/81wmxkmnbwL.jpg" },
       { id: 4, titulo: "Capitã Marvel",avaliacao: 2,   estoqueDisponivel: 3,descricao: "Um filme de capitãs", valor: 40, imagem: "https://images-na.ssl-images-amazon.com/images/I/81wmxkmnbwL.jpg" },
       { id: 5, titulo: "Hulk",avaliacao: 2,   estoqueDisponivel: 3,descricao: "Um filme de força", valor: 10, imagem: "https://br.web.img2.acsta.net/c_215_290/pictures/210/485/21048566_20131010182211313.jpg" },
      { id: 6, titulo: "Hulk",avaliacao: 2,   estoqueDisponivel: 3, descricao: "Um filme de força", valor: 10, imagem:"https://br.web.img2.acsta.net/c_215_290/pictures/210/485/21048566_20131010182211313.jpg" }
     ],
     filmes: ['Vingadores', 'Homem de Ferro', 'Hulk', 'Pantera negra']
   }
 },
  methods: { 
    filtra5estrelas(){
      this.filmes_obj = this.filmes_obj.filter(elem => elem.avaliacao === 5)
      return this.filmes_obj
    },
    mostrarCarrinho() {
      this.$router.push({name : "carrinho"})
    },
    removeFilmeLista: function(id){
      this.filmes_obj = this.filmes_obj.filter(elem => elem.id != id)
      return this.filmes_obj
    },
    adicionarAoCarrinho: function(filme) {
      this.carrinho.push(filme.id);
    },quantidadeNoCarrinhoPorFilme: function(filme) {
      return this.carrinho.filter(elem => elem === filme.id).length;
   },
   validarPermissaoParaAdicionarNoCarrinho: function(filme) {
     return filme.estoqueDisponivel > this.quantidadeNoCarrinhoPorFilme(filme);
    }
  },
  computed: {
    quantidadeNoCarrinho: function() {
      return this.carrinho.length;
    },
    filmesOrdenados: function(){
      let filmesOrd = this.filmes_obj
      filmesOrd.sort(function (a, b) {
        if (a.titulo > b.titulo) {
          return 1;
        }
        if (a.titulo < b.titulo) {
          return -1;
        }
        // a must be equal to b
        return 0;
      });
      return this.filmes_obj    
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .cards{
    justify-content: space-between;
    display: flex;
    flex-wrap: wrap;
  }
  .home{
      align-items: center;
      margin: 24px;
  }
  .card{
    margin: 24px;
  }
  #aberta {
    color: blue;
  }
  
  #proxima-fechar {
    color: orange;
  }
  
  #fechada {
    color: red;
  }
  </style>