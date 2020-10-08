<template>
    <container :content="content" :isRoot="true"/>
</template>
<script>
require('bootstrap')
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
