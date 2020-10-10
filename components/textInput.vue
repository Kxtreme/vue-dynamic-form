<template>
    <div class="input-text-container">
        <input class="form-control col-11 align-left" v-model="name" @input="updateName()" placeholder="Field name">
        <a class="btn align-right" @click="$emit('selfDestroy')"><minus-circle-outline /></a>
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
