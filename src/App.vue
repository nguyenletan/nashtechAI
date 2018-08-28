<template>
    <div id="app">
       <!-- <div id="nav">
            <router-link to="/">Nha</router-link>
            |
            <router-link to="/about">Gioi Thieu</router-link>
        </div>-->
        <router-view/>

        <!--<PokeList :handle-on-click="handleOnClick"></PokeList>

        <DetailView :pokemon="pokemon"></DetailView>-->

    </div>
</template>

<script>
import DetailView from "./components/DetailView";
import PokeList from "./components/PokeList";
import Pokemon from "./Pokemon";

export default {
  name: "app",
  data: function() {
    return {
      pokemon: []
    };
  },

  methods: {
    handleOnClick: function(id) {
      fetch(`https://pokeapi.co/api/v2/pokemon/${id}/`)
        .then(res => res.json())
        .then(data => {
          this.pokemon = new Pokemon(data);
          console.log(this.pokemon);
        })
        .catch(err => console.log(err));
    }
  },
  components: {
    PokeList,
    DetailView
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /*display: flex;
        align-items: center;
        justify-content: center;
        width: 980px;
        height: 92vh;
        padding: 15px;
        margin: 4vh auto;
        background-color: #42B983;
        border-radius: 5px;
        box-shadow: 0 14px 45px rgba(0, 0, 0, 0.22), 0 18px 45px rgba(0, 0, 0, 0.22);*/

  #nav {
    padding: 30px;
    a {
      font-weight: bold;
      color: #2c3e50;
      &.router-link-exact-active {
        color: #42b983;
      }
    }
  }
}
</style>
