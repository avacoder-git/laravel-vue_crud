<template>
    <div class="w-25">
        <div class="mb-3">
            <input type="text" id="name" v-model="name" class="form-control">
        </div>
        <div class="mb-3">
            <input type="number" id="age" v-model="age" class="form-control">
        </div>
        <div class="mb-3">
            <input type="text" id="job" v-model="job" class="form-control">
        </div>
        <div class="mb-3">
            <input type="submit" @click.prevent="addPerson" class="btn btn-primary" value="+">
        </div>
        <SomeComponent :obj="obj"></SomeComponent>
    </div>
</template>

<script>

import SomeComponent from "./SomeComponent";
export default {
    name: "CreateComponent",
    components: {SomeComponent},
    data() {
        return {
            name: null,
            age: null,
            job: null,
            obj: {
                color: "Yellow",
                number: 20,
                isPublished: true
            }
        }
    },

    methods: {
        addPerson(){
            axios.post('/api/people', {
                name: this.name,
                age: this.age,
                job: this.job,
            }).then( res => {
                this.name = null
                this.age = null
                this.job = null
                this.$parent.$refs.index.getPeople()
            })
        },

    },

    mounted() {
    }

}
</script>

<style scoped>

</style>
