<template>
  <div class="box pf">
    <a href="https://github.com/Titivoot/elfi-bot" target="_blank" class="pf-item" v-for="project in projects" :key="project.id">
        <p class="pf-title">{{ project.name }}</p>
        <p class="pf-details">{{ project.description }}</p>
    </a>
  </div>
</template>

<script>
export default {
    data() {
        return {
            projects: []
        }
    },
    mounted() {
        this.fetch()
    },
    methods: {
        async fetch() {
            let repos = await this.$axios.$get('https://api.github.com/users/titivoot/repos')
            repos.sort((a,b) => {
                return new Date(b.created_at) - new Date(a.created_at);
            })
            return this.projects = repos.slice(0,4)
        }    
    }
}
</script>
