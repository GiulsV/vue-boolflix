<template>
  <div id="app">
    <HeaderCompVue 
     @sendToApp="getSearch($event)" />
    <MainCompVue :arrayFilms="filmList"/>
  </div>
</template>

<script>
import HeaderCompVue from './components/HeaderComp.vue';
import MainCompVue from './components/MainComp.vue';


export default {
  name: "App",
  components: {
    HeaderCompVue,
    MainCompVue
  },
  data() {
    return {
      filmList: [],
    }
  },
  methods: {
    getSearch(value) {
      this.filmList = value;
      console.log(this.filmList);
    },
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
