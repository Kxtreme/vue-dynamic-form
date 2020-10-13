<template>
    <div class="input-text-container alert alert-primary">
        <input class="form-control col-11 align-left" v-model="content[selectedLanguage]" placeholder="Field name">
        <a class="btn align-right col-1" @click="$emit('selfDestroy')"><minus-circle-outline /></a>
    </div>
</template>

<script>
import '../styles.css';
import MinusCircleOutline from 'vue-material-design-icons/MinusCircleOutline.vue';

    export default {
        props: {
            languages: {
                type: Array,
                required: true
            },
            selectedLanguage: {
                type: String,
                required: true
            },
            content: {
                type: Object,
                required: true
            },
        },
        data() {
            return {
                name: ''
            };
        },
        components: {
            MinusCircleOutline
        }
    }
</script>
