<template>
  <div id="app">
    <HeaderCompVue
      @sendToApp="getSearch($event)"
    />
    <MainCompVue 
      :arrayFilms="filmList"
    />
  </div>
</template>

<script>
import HeaderCompVue from '@/components/HeaderComp.vue';
import MainCompVue from '@/components/MainComp.vue';


export default {
  name: "App",
  components: {
    HeaderCompVue,
    MainCompVue
  },
  data() {
    return {
      filmList: {
        film: [],
        series: []
      },
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

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  // color: #2c3e50;
  // margin-top: 60px;
}
</style>
