<template>
    <div>

        <div class="p-5 ">
            <CreateComponent ref="create"></CreateComponent>
            <IndexComponent ref="index"></IndexComponent>


        </div>


    </div>
</template>

<script>
import CreateComponent from "./CreateComponent";
import IndexComponent from "./IndexComponent";
import SomeComponent from "./SomeComponent";

export default {
    name: "PostComponent",

    components: {
        SomeComponent,
        CreateComponent,
        IndexComponent
    },

    mounted() {
        this.$refs.index.getPeople()
    },


    data() {
        return {}
    },

    methods: {

    },

    computed: {}

}
</script>

<style scoped>

</style>
