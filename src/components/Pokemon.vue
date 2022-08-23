<template>
    <div>
        <h1>{{num}} {{upper(name)}}</h1>
        <small>{{url}}</small>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            pokemon: {}
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {
        upper(value){
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName
        }
    },
    created: function(){
        axios.get(this.url).then(response =>{
            this.pokemon.type = response.data.types[0].type.name
            this.pokemon.front = response.data.sprites.front_default
            this.pokemon.back = response.data.sprites.back_default
        }
    )
}
  
}   
</script>

<style>

</style>
