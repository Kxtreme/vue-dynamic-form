<template>
    <div>
        <div class="alert alert-info">
                <div v-for="c in content" :key="c.id">
                    <container v-if="c.type=='container'" :content="c.content" k/>
                </div>
            <div class="icons">
                <a class="btn btn-default" @click="addContainer">Add Container</a>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            content: {
                type: Array,
                required: true
            }
        },
        methods: {
            generateRandomId() {
                return Math.random().toString(36).substring(7)
            },
            addContainer() {
                this.content.push({
                    type: 'container',
                    content: [],
                    id: this.generateRandomId()
                })
            }
        },
        components: {
            container: () => import('./container')
        }
    }
</script>
