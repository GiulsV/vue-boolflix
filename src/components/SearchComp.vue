<template>
  <div class="search-container">
      <input @keyup.enter="sendInput()" type="text" v-model="searchText">
      <button @click="sendInput()">Cerca</button>
  </div>
</template>

<script>
import axios from 'axios';
// api_key=7d280c404bb1d6acb95e9350180c6a30
export default {
    name: "SearchComp",
    data() {
        return {
            filmApiQuery: "https://api.themoviedb.org/3/search/movie?api_key=7d280c404bb1d6acb95e9350180c6a30&language=it-IT&query=",
            seriesApiQuery: "https://api.themoviedb.org/3/search/tv?api_key=7d280c404bb1d6acb95e9350180c6a30&language=it-IT&query=",
            searchText: "",
            filmList: {
                film: [],
                series: [],
                 firstSearch: false
            },
        }
    },
    methods: {
        sendInput() {
            if(this.searchText.trim() != "") {
                axios.get(this.filmApiQuery+this.searchText)       //film
                .then(res => {
                    
                    this.filmList.firstSearch = true;
                    this.filmList.film = res.data.results;
                    
                    axios.get(this.seriesApiQuery+this.searchText)  //serie TV
                        .then(res => {
                            this.filmList.series = res.data.results;
                            this.$emit("sendSearch", this.filmList);
                        })
                        .catch(err => console.log(err))
                })
                .catch(err => console.log(err))
            }
            else{
                this.filmList = {
                    film: [],
                    series: [],
                    firstSearch: false
                };
                this.$emit("sendSearch", this.filmList);
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    .search-container {
        display: flex;
        align-items: center;
        height: 100%;
        // input {
        //     width: 300px;
        //     height: 40%;
        //     background-color: rgba(0,0,0,0);
        //     border: 1px solid rgb(101, 109, 224);
        //     outline: none;
        //     color: white;
        //     padding: 0 1rem;
        // }

        input {
        font-family: sans-serif;
        padding: 0 1rem;
        border: 3px solid white;
        color: white;
        text-indent: 15px;
        outline: none;
        border-radius: 4px;
        background: none;
        border: 1px solid rgb(101, 109, 224);
        transition: .3s;
        width: 300px;
        height: 40%;
        }

        input:focus {
            box-shadow: 0 0 5px rgb(120, 128, 240),
                        0 0 15px rgb(120, 128, 240);
            border: 1px solid rgb(120, 128, 240);
        }

        button {
            height: 40%;
            border: none;
            background-color: rgb(101, 109, 224);
            text-transform: uppercase;
            color: white;
            font-size: 0.8rem;
            cursor: pointer;
            padding: 5px;
            margin-left: 5px;
        }
    }

</style>