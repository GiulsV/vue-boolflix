<template>
  <header>
      <div class="header-container">
        <h1>Boolflix</h1>
        <SearchComp
            @sendSearch="setSearch($event)"
        />
      </div>
  </header>
</template>

<script>
import SearchComp from '@/components/SearchComp.vue';

export default {
    name: "HeaderCompVue",
    components: {
        SearchComp,
    },
    data() {
        return {
            filmList: {
                film: [],
                series: [],
                firstSearch: false
            },
        }
    },
    methods: {
        setSearch(value) {

            this.filmList = value;
            this.sendSearch();
        },
        sendSearch() {
            this.$emit("sendToApp", this.filmList);
        }
    }
}
</script>

<style lang="scss" scoped>
     header {
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgb(0, 0, 0);
        position: sticky;
        z-index: 100;
        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: auto;
            width: 90%;
            height: 70px;
            h1 {
                color: red;
                font-size: 3.5rem;
                letter-spacing: 3px;
            }
        }
        
    }
</style>
