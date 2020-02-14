
<template>
  <div class="hello">
    
    
    
  </div>
</template>

<script>
export default {
  name: 'Fatorial',
  data(){
    return {n:5}
  }, methods : {
    fatorial : function (){
      let n = this.n
      let resultado = 1
      for (let i=1; i<n+1; i++){
        resultado=resultado*i
      }
      return resultado
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
