<template>
    <div v-for="result in results"  :key=result">

    </div>

</template>
<script>
    export default {
        props: {
            result: {
                type: Array,
                required: true
            }
        },
        methods: {

        }
    }
</script>
