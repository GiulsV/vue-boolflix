<template>
  <div class="card-container">
      <ul>
          <li>Titolo: {{film.title}}</li>
          <li>Titolo Originale: {{film.original_title}}</li>
          <li>Lingua Originale: {{film.original_language}}</li>
          <li>Voto: {{film.vote_average}}</li>
      </ul>
  </div>
</template>

<script>
export default {
    name: "FilmComp",
    props: {
        film: Object,
    }
}
</script>

<style lang="scss" scoped>
ul{
    list-style: none;
}
</style>