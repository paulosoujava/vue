<template>
  <div id="app">
    <h1 class="title is-1">POKEMON VUE</h1>
    <div class="field" style="margin-left:30px; margin-right:30px">
      <div class="control">
        <input class="input is-large" type="text" placeholder="buscar pokemon" v-model="search" />
      </div>
      <br />
    
    </div>
    <div class="columns is-multiline is-mobile">
  
    <div v-for="(poke, idx) in resulSearch" :key="idx" class="column is-one-quarter">
      <div >
        <Pokemon  :name="poke.name" :url="poke.url" :num="idx+1" />
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data(){
    return{
    pokemons:[],
    search:''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=15&offset=0").then(
      res =>{ console.log(res.data.results);
      this.pokemons = res.data.results;
      })
  },
  components:{
    Pokemon
  },
  computed:{
    resulSearch: function(){
      if(!this.search){
        return this.pokemons
      }else{
        return this.pokemons.filter( (pk)=>{
          return pk.name.match(this.search)
        })
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
