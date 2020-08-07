<template>
    <div class="card breed-card" style="width: 100%;">
        <img :src="breed.picture" class="card-img-top img-fluid" >
        <div class="card-body">
        <h5 class="card-title">{{ breed.name }}</h5>
        <p class="card-text">
            {{ breed.description }}
        </p>
        <div class="action-buttons">
            <nuxt-link :to="`/breeds/${breed.id}/`" class="btn btn-sm btn-success"> View </nuxt-link>
            <nuxt-link :to="`/breeds/${breed.id}/edit/`" class="btn btn-sm btn-primary"> Edit </nuxt-link>
            <button @click="onDelete(breed.id)"  class="btn btn-sm btn-danger">Delete</button>
        </div>
        </div>
    </div>
</template>

<script>
export default {
    // props: {
    //     breed: {
    //         type: Object,
    //     },
    //     onDelete : {
    //         type: Function,
    //     }
    // } 
    props : ["breed", "onDelete"]
}
</script>

<style scoped>
.breed-card {
    box-shadow: 0 1rem 1.5rem rgba(0,0,0,.6);
    padding: 10px;
}
</style>