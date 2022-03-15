<template>
    <div>

        <table class="table ">
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Age</th>
                <th>Job</th>
                <th>Edit</th>
                <th>Delete</th>
            </tr>
            <template v-for="person in people">
                <ShowComponent :person="person" :ref="`show_${person.id}`"></ShowComponent>
                <EditComponent :person="person" :ref="`edit_${person.id}`"></EditComponent>
            </template>


        </table>

    </div>
</template>

<script>

import EditComponent from "./EditComponent";
import ShowComponent from "./ShowComponent";

export default {
    name: "IndexComponent",
    components: {ShowComponent, EditComponent},
    data() {
        return {
            people: null,
            editPersonId: null,
            name: null,
            age: null,
            job: null
        }
    },

    mounted() {
    },
    methods: {
        getPeople() {
            axios.get('/api/people').then(result => {
                this.people = result.data
            })
        },

        changeEditPersonId(id, name, age, job) {
            this.editPersonId = id
            let editName = `edit_${id}`
            let fullEditName = this.$refs[editName][0]
            fullEditName.name = name
            fullEditName.age = age
            fullEditName.job = job
        },

        updatePerson(id) {
            this.editPersonId = null
            axios.patch(`/api/people/${id}`, {name: this.name, age: this.age, job: this.job}).then(result => {
                this.getPeople()
            })
        },

        deletePerson(id) {
            axios.delete(`/api/people/${id}`).then(result => {
                this.getPeople()
            })
        },

        isEdit(id) {
            return this.editPersonId === id
        },
        indexLog() {
            console.log("This is an index component");
        }
    },

    computed: {}

}
</script>

<style scoped>

</style>
