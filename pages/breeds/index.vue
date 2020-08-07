<template>
    <main class="container">
        <div class="row">
          <div class="col-12 text-right mb-4">
              <div class="d-flex justify-content-between">
              <h3>Cat Breeds</h3>
              <nuxt-link to="/breeds/add" class="btn btn-info">Add Breed</nuxt-link>
              </div>
          </div>

          <template v-for="breed in breeds"> 
            <div :key="breed.id" class="col-lg-3 col-md-4 col-sm-6 mb-4">
              <BreedCard :onDelete="deleteBreed" :breed="breed" />
            </div>
          </template>

        </div>
  </main>
</template>

<script>
import BreedCard from "~/components/BreedCard.vue";

export default {
  head() {
    return {
      title: "Breeds list"
    };
  },
  components: {
    BreedCard
  },
  async asyncData({ $axios, params }) {
    try {
      let breeds = await $axios.$get('/breeds/');
      return { breeds : breeds.results };
    } catch (e) {
      return { breeds: [] };
    }
  },
  data() {
    return {
      breeds: []
    };
  },
  methods: {
    async deleteBreed(breed_id) {
      try {
        await this.$axios.$delete(`/breeds/${breed_id}/`);
        let newBreeds = await this.$axios.$get('/breeds/');
        this.breeds = newBreeds.results;
        console.log(this.breeds);
      } catch (e) {
        console.log(e);
      }
    }
  }
}
</script>

<style scoped>

</style>