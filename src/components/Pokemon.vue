<template>
  <div>
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <figure class="image is-48x48">
              <img
                :src="pokemon.front"
                alt="Placeholder image"
              />
            </figure>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ upper(name) }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
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
  },
  created: function () {
    axios.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
    });
  },
};
</script>

<style>
.card{
    margin: 10px
}
</style>
