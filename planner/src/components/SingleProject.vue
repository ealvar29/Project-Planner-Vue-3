<template>
    <div class="project">
        <div class="actions" @click="">
            <h3>{{ project.title }}</h3>
            <div class="icons">
                <span class="material-icons" >done</span>
                <span class="material-icons" >edit</span>
                <span @click="deleteDetails" class="material-icons" >delete</span>
            </div>
        </div>

        <div class="details" v-if="isHidden">
        <p>{{ project.details }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['project'],
        data() {
            return {
                isHidden: false,
                uri: 'http://localhost:3000/projects/' + this.project.id
            }
        },
        methods:{
            hideDetails() {
                    this.isHidden = !this.isHidden
                    console.log(this.isHidden)
            },
            deleteDetails(){
                fetch(this.uri, {method: 'DELETE'})
                .then(() => this.$emit('delete', this.project.id))
                .catch(err => console.log(err))
            }
        }
    }
</script>

<style scoped>
  .project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;
  }
  h3 {
    cursor: pointer;
  }
  .actions {
      display: flex;
      justify-content: space-between;
      align-items: center;
  }
   .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
</style>