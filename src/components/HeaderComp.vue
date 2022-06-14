<template>
  <header>
      <SearchComp
        @sendSearch="setSearch($event)"
      />
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
                series: []
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
        width: 100%;
        height: 80px;
        border-bottom: 1px solid black;
    }
</style>
