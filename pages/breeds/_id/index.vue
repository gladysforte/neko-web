<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h2 class="mb-3 display-4 text-uppercase">{{ breed.name }}</h2>
            </div>

            <div class="col-md-6 mb-4">
                <img class="img-fluid" style="width: 400px; border-radius: 10px;box-shadow: 0 1rem 1rem rgba(0,0,0,.7);"
                    :src="breed.picture" alt>
            </div>

            <div class="col-md-6">
                <div class="breed-details">
                    <h4>Description</h4>
                    <p>{{ breed.description }}</p>
                    <h4>Alternative Name</h4>
                    <p>{{ breed.alternative_name }}</p>
                    <h4>Origin</h4>
                    <p>{{ breed.origin }}</p>
                    <h4>Description</h4>
                    <textarea class="form-control" rows="10" v-html="breed.description" disabled />
                    <h4>Lifespan</h4>
                    <p>{{ breed.lifespan }}</p>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    head() {
        return {
            title: "View Recipe"
        };
    },
    async asyncData({ $axios, params }) {
        try {
            let breed = await $axios.$get(`/breeds/${params.id}`);
            return {breed};
        } catch (error) {
            return {breed: []};
        }
    },
    data() {
        return {
            breed: {
                name: "",
                picture: "",
                alternative_name: "",
                origin: "",
                lifespan: "",
                description: "",
            }
        };
    }

}
</script>

<style scoped>

</style>