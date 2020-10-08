<template>
    <div>
        <input class="form-control" v-model="name" @input="updateName()">
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name: ''
            };
        },
        methods: {
            updateName(){
                this.$emit('input', this.name)
            }
        }
    }
</script>
