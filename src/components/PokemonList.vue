<template>
  <div class="list" v-if="loaded">
    <article v-for="item in pokemonsFiltered" :key="item.name" @click="showPokemonDetail(item.url)">
      <img :src="imgs + item.name + '.png'">
      <h3>{{ item.name }}</h3>
    </article>
  </div>
</template>

<script>
import conf from "../config/config.json";
import axios from 'axios';
const _ = require('lodash');
export default {
  props: ['searched', 'url'],
  data: function () {
    return {
      pokemons: null,
      imgs: conf['IMG_URL'],
      loaded: false,
    }
  },
  methods: {
    showPokemonDetail: function(url) {
      this.$emit('showPokemonDetailEmit', url);
    },
  },
  beforeCreate: async function () {
    await axios.get(conf['API_URL']+'/pokemon').then((response) => {
      this.pokemons = response.data;
      this.loaded = true;
      console.log(response.data)
    })
  },
  watch: {
    url() {
      axios.get(this.url).then((response) => {
        this.pokemons = response.data;
      })
    }
  },
  computed: {
    pokemonsFiltered: function () {
      if (this.searched == "") {
        return this.pokemons.results;
      } else {
        var self = this;
        return this.pokemons.results.filter(function (pokemon) {
          return _.includes(pokemon.name.toLowerCase(), self.searched.toLowerCase());
        });
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

