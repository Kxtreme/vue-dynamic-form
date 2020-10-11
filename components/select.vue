<template>
    <div class="alert alert-primary">
            <div class="form-row">
                <div class="col-auto col-11 align-left">
                    <div class="col-2">
                        <input class="form-control form-control-sm" @input="updateProperties" v-model="properties.description" placeholder="Description">
                    </div>
                </div>
                <a class="btn align-right col-1" @click="$emit('selfDestroy')"><delete-circle-outline /></a>
            </div>
            <div class="form-row" v-for="(c, index) in content">
                <input class="form-control col-11" v-model="c.name" placeholder="Option name">
                <a v-if="index==0" class="btn align-right col-1" @click="addOption"><plus-circle-outline /></a>
                <a v-else="" class="btn align-right col-1" @click="deleteOption(c)"><minus-circle-outline /></a>
            </div>
    </div>
</template>

<script>
import '../styles.css';
import Utils from '../utils.js';
import MinusCircleOutline from 'vue-material-design-icons/MinusCircleOutline.vue';
import PlusCircleOutline from 'vue-material-design-icons/PlusCircleOutline.vue';
import DeleteCircleOutline from 'vue-material-design-icons/DeleteCircleOutline.vue';
    export default {
        props: {
            content: {
                type: Array,
                required: true
            }
        },
        data() {
            return {
                properties: {
                    description: ''
                }
            };
        },
        methods: {
            addOption() {
                this.content.push({
                    name: '',
                    id: Utils.generateRandomId()
                })
            },
            deleteOption(item) {
                this.content.splice(this.content.indexOf(item), 1);
            },
            updateProperties(){
                this.$emit('input', this.properties)
            }
        },
        mounted() {
            this.addOption()
        },
        components: {
            MinusCircleOutline,
            PlusCircleOutline,
            DeleteCircleOutline
        }
    }
</script>
