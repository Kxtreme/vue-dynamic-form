<template>
    <div>
        <input class="form-control col-11 align-left" v-model="name" @input="updateName()">
        <a class="btn align-right" @click="$emit('selfDestroy')"><minus-circle-outline /></a>
    </div>
</template>

<script>
import MinusCircleOutline from 'vue-material-design-icons/MinusCircleOutline.vue';

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
        },
        components: {
            MinusCircleOutline
        }
    }
</script>
