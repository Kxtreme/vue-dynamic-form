<template>
    <div class="input-text-container alert alert-primary">
        <input class="form-control col-11 align-left" v-model="name" @input="updateName()" placeholder="Field name">
        <a class="btn align-right col-1" @click="$emit('selfDestroy')"><minus-circle-outline /></a>
    </div>
</template>

<script>
import '../styles.css';
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
