<template>
  <form @submit.prevent="EditProject">
        <label>Title:</label>
        <input required v-model="title" type="text" />
        <label>Details:</label>
        <textarea required v-model="details"></textarea>
        <button>Add Project</button>
    </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: `http://localhost:3000/projects/${this.id}`
    }
  },
  methods:{
    EditProject() {
      let project = {
        title: this.title,
        details: this.details
      }
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
      .then(() => {
        this.$emit('complete', this.project.id)
      })
      .then(() => {
        this.$router.push('/')
      })
      .catch(err => console.log(err))
    }
  },
  mounted(){
    fetch(this.uri)
    .then(res => res.json())
    .then(data => {
      this.title = data.title,
      this.details = data.details
    })
  }
}
</script>

<style>

</style>