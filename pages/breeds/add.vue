<template>
  <main class="container my-5">
    <div class="row">
      <div class="col-12 text-center my-3">
        <h2 class="mb-3 display-4 text-uppercase">{{ breed.name }}</h2>
      </div>
      <div class="col-md-6 mb-4">
        <img
          v-if="preview"
          class="img-fluid"
          style="width: 400px; border-radius: 10px; box-shadow: 0 1rem 1rem rgba(0,0,0,.7);"
          :src="preview"
          alt
        >
        <img
          v-else
          class="img-fluid"
          style="width: 400px; border-radius: 10px; box-shadow: 0 1rem 1rem rgba(0,0,0,.7);"
          src="@/static/images/placeholder.png"
        >
      </div>
      <div class="col-md-4">
        <form @submit.prevent="submitBreed">
          <div class="form-group">
            <label for>Breed Name</label>
            <input type="text" class="form-control" v-model="breed.name">
          </div>
          <div class="form-group">
            <label for>Alternative Name</label>
            <input type="text" class="form-control" v-model="breed.alternative_name">
          </div>
          <div class="form-group">
            <label for>Origin</label>
            <input type="text" class="form-control" v-model="breed.origin">
          </div>
          <div class="form-group">
            <label for>Description</label>
            <input v-model="breed.description" type="text" class="form-control">
          </div>
          <div class="form-group">
            <label for>Lifespan</label>
            <input v-model="breed.lifespan" type="text" class="form-control">
          </div>
          <div class="form-group">
            <label for>Breed picture</label>
            <input type="file" name="file" @change="onFileChange">
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
      </div>
    </div>
  </main>
</template>
<script>
export default {
  head() {
    return {
      title: "Add Breed"
    };
  },
  data() {
    return {
      breed: {
        name: "",
        picture: "",
        description: "",
        alternative_name: "",
        origin: "",
        lifespan: "",
      },
      preview: ""
    };
  },
  methods: {
    onFileChange(e) {
      let files = e.target.files || e.dataTransfer.files;
      if (!files.length) {
        return;
      }
      this.breed.picture = files[0];
      this.createImage(files[0]);
    },
    createImage(file) {
      // let image = new Image();
      let reader = new FileReader();
      let vm = this;
      reader.onload = e => {
        vm.preview = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    async submitBreed() {
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.breed) {
        formData.append(data, this.breed[data]);
      }
      try {
        let response = await this.$axios.$post("/breeds/", formData, config);
        this.$router.push("/breeds/");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>
<style scoped>
</style>