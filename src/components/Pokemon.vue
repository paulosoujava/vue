<template>
<div>
   <div class="card">
      <div class="card-image">
      <figure @click="changeSprint" style="cursor:pointer">
        <img :src="currentImg" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure @click="changeSprint" style="cursor:pointer">
            <img :src="otherImg" alt="Placeholder image">
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-4">{{name | upper}}</p>
          <p class="subtitle is-6">Poder:{{num}}</p>
        </div>
      </div>

      <div class="content">
        <p class="subtitle is-6">Tipo: {{pokemon.type}}</p>
      </div>
    </div>
   </div>
</div>

</template>
<script>
import axios from "axios";
export default {
  created: function(){
    axios.get(this.url).then( res =>{
      this.pokemon.type = res.data.types[0].type.name
      this.pokemon.front = res.data.sprites.front_default
      this.pokemon.back = res.data.sprites.back_default
      this.currentImg = this.pokemon.front
      this.otherImg = this.pokemon.back
    })
  },
  data(){
    return{
      isFront: true,
      currentImg: '',
      otherImg: '',
      pokemon:{
        type: '',
        front:'',
        back:'',
      }
    }
  },
  props:{
    name: String,
    url: String,
    num: Number
  },
  filters:{
    upper: function(v){
      var newName = v[0].toUpperCase() + v.slice(1);
      return newName;
    }
  }, methods:{
    changeSprint : function(){
      if(this.isFront){
        this.isFront = false
        this.currentImg = this.pokemon.back;
        this.otherImg = this.pokemon.front;
      }else{
        this.isFront = true
        this.currentImg = this.pokemon.front;
        this.otherImg = this.pokemon.back;
      }
    }
  }
}
</script>