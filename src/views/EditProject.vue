<template>
    <form @submit.prevent="handleSubmit">
    <label>Title: </label>
    <input type="text" v-model="title" required>
    <label>Details: </label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            title : '',
            details : '',
            url: 'https://62bd66d0c5ad14c110bdc696.mockapi.io/projects/' + this.id
        }
    },
    mounted(){
        fetch(this.url)
        .then(res => res.json())
        .then(data => {
            this.title = data.title
            this.details = data.details
        }).catch(err => console.log(err))
    },

    methods: {
        handleSubmit(){
            let project = {
                title : this.title,
                details : this.details
            }
            console.log(project)
            fetch(this.url, {
                method : 'PATCH',
                headers : { 'Content-Type' : 'application/json' },
                body : JSON.stringify(project)
            }).then(() => this.$router.push('/'))
            .catch(err => console.log(err))
        }
    }
}
</script>

<style>

</style>