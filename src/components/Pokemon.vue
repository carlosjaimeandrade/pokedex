<template>
  <div>
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <figure class="image is-90x90">
              <img :src="currentImg" alt="Placeholder image" />
            </figure>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ upper(name) }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
          <button @click="mudarSprit()" class="button is-light">{{girar}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      girar: "Ver atrás",
      isFront: true,
      currentImg: "",
      pokemon: {},
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  methods: {
    upper(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
    mudarSprit: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
        this.girar = "Ver frete"
      }else{
        this.isFront = true;
        this.currentImg = this.pokemon.front;
        this.girar = "Ver atrás"
      }
    },
  },
  created: function () {
    axios.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
};
</script>

<style>
.card {
  margin: 10px;
}
</style>
