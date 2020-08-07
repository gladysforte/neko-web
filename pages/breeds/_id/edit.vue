<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h2 class="mb-3 display-4 text-uppercase">{{ breed.name }}</h2>
            </div>
            <div class="col-md-6 mb-4">
                <img v-if="!preview" class="img-fluid" style="width: 400px; border-radius: 10px; box-shadow: 0 1rem 1rem rgba(0,0,0,.7);"
                    :src="breed.picture">
                <img v-else class="img-fluid" style="width: 400px; border-radius: 10px; box-shadow: 0 1rem 1rem rgba(0,0,0,.7);"  :src="preview">
            </div>
            <div class="col-md-4">
                <form @submit.prevent="submitBreed">
                    <div class="form-group">
                        <label for>Breed Name</label>>
                        <input type="text" class="form-control" v-model="breed.name">
                    </div>
                    <div class="form-group">
                        <label>Description</label>
                        <input type="text" v-model="breed.description" class="form-control" name="Description">
                    </div>
                    <div class="form-group">
                        <label for>Picture</label>
                        <input type="file" @change="onFileChange">
                    </div>
                    <button type="submit" class="btn btn-success">Save</button>
                </form>
            </div>
        </div>

    </main>
</template>

<script>
export default {
    head() {
        return {
            title: "Edit Recipe"
        }
    },
    async asyncData({ $axios, params }) {
        try {
            let breed = await $axios.$get(`/breeds/${params.id}`);
            return { breed };
        } catch (error) {
            return { breed: [] };
        }
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
            this.breed.picture = files[0]
            this.createImage(files[0]);
        },
        createImage(file) {
            let reader = new FileReader();
            let vm = this;

            reader.onload = e => {
                vm.preview = e.target.result;
            };
            reader.readAsDataURL(file);
        },
        async submitBreed() {
            let editedBreed = this.breed;
            if (editedBreed.picture.indexOf("http://") != -1){
                delete editedBreed["picture"]
            }
            const config = {
                headers: { "content-type": "multipart/form-data" }
            };
            let formData = new FormData();
            for (let data in editedBreed) {
                formData.append(data, editedBreed[data]);
            }
            try {
                let response = await this.$axios.$patch(`/breeds/${editedBreed.id}/`, formData, config);
                this.$router.push("/breeds/");
            } catch (e) {
                console.log(e);
            }
        }
    },
}
</script>

<style scoped>

</style>