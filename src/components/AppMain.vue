<script>
import axios from "axios";
import AppCard from "./AppCard.vue";
export default {
    name: 'AppMain',
    components: {
    AppCard,
},
    data() {
        return {
            laravelUrl: "http://127.0.0.1:8000",
            projects: []
        }
    },
    created() {
        this.getProjects();
    },
    methods: {
        getProjects() {
            axios.get(`${this.laravelUrl}/api/projects`)
            .then(resp => {
                this.projects = resp.data.results;
            });
            console.log(this.projects);
        }
    }
}
</script>

<template>
<div class="container">
    <h2 class="text-center">I nostri progetti</h2>
    <div class="row justify-content-center">
        <div class="col-8">
            <AppCard :project="project" v-for="project in projects" :key="project.id" />
        </div>
    </div>
</div>
</template>

<style lang="scss">
@use "../styles/general.scss" as *;
</style>