<template>
  <div class="container">
    <PokemonSearch @searchPokemonEmit="setPokemonSearch"/>
    <PokemonDetail :pokemonUrl='url' :visible='visible' @close="close"/>
    <PokemonList @showPokemonDetailEmit="show" :searched='searched' :url="listUrl"/>
    <PokemonListTabs @Previous="previous()" @Next="next()"></PokemonListTabs>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";
import PokemonListTabs from "../components/PokemonListTabs.vue";
import conf from "../config/config.json";

export default {
  data: function () {
    return {
      url: "https://pokeapi.co/api/v2/pokemon/1",
      listUrl: conf['API_URL']+'/pokemon',
      visible: false,
      searched: "",
      page: 0,
      count: 1154
    }
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
    PokemonListTabs
  },
  methods: {
    show: function(url) {
      this.url = url;
      this.visible = true;
    },
    close: function() {
      this.visible = false;
    },
    setPokemonSearch: function(val) {
      this.searched = val;
    },
    previous: function() {
      if (this.page - 1 >= 0) {
        this.page -= 1;
        this.updateUrl();
      }
    },
    next: function() {
      if (this.page + 1 <= this.count / 20) {
        this.page += 1;
        this.updateUrl();
      }
    },
    updateUrl: function() {
      this.listUrl = conf['API_URL']+'/pokemon?offset='+this.page*20+"&limit=20";
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>