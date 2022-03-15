<template>


    <tr :class="this.$parent.isEdit(person.id)?'': 'd-none' ">
        <td>{{ person.id }}</td>
        <td><input v-model="name" type="text" class="form-control"></td>
        <td><input v-model="age" type="text" class="form-control"></td>
        <td><input v-model="job" type="text" class="form-control"></td>
        <td><a href="" @click.prevent="updatePerson(person.id)" class="btn btn-primary">Update</a></td>
    </tr>

</template>

<script>

export default {
    name: "EditComponent",


    data() {
        return {
            name: null,
            age: null,
            job: null
        }
    },
    props: [
        'person'
    ],

    mounted() {

    },
    methods: {
        updatePerson(id) {
            this.$parent.editPersonId = null
            axios.patch(`/api/people/${id}`, {name: this.name, age: this.age, job: this.job}).then(result => {
                this.$parent.getPeople()
            })
        },
    },

    computed: {}

}
</script>

<style scoped>

</style>
