<template>
    <button class="poke-cell" v-bind:style="style"
            :id="id"
            @click="onClick"
    >

    </button>
</template>


<script>
import sprites from "../assets/sprites.png";

export default {
  name: "PokeCell",

  data: function() {
    return {
      style: { backgroundImage: "", backgroundPosition: "" },
      id: ""
    };
  },
  props: {
    pokeClass: {
      id: "",
      backgroundPosition: ""
    },
    handleOnClick: {}
  },
  created: function() {
    this.style = {
      backgroundImage: `url(${sprites})`,
      backgroundPosition: this.pokeClass.backgroundPosition
    };
    this.id = this.pokeClass.id;
  },
  methods: {
    onClick: function() {
      //console.log(this.id);
      this.handleOnClick(this.id);
    }
  }
};
</script>


<style>
.poke-cell {
  width: 120px;
  height: 120px;
  margin: 10px;
  background: #fff no-repeat;
  border: none;
  border-radius: 5px;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.16);
}
</style>
