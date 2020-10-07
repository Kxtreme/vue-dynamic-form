<template>
    <container :content="content"/>
</template>
<script>
import container from './components/container.vue'
    export default {
        props: {
            content: {
                type: Array,
                required: true
            }
        },
        components: {
            container
        }
    }
</script>
