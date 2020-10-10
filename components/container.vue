<template>
    <div>
        <div class="alert alert-info">
            <div class="form-row align-items-center" v-if="!isRoot">
                <div class="col-auto">
                    <div class="form-check mb-2">
                        <input class="form-control form-control-sm" @input="updateProperties" v-model="properties.description" placeholder="Description">
                    </div>
                </div>
                <div class="col-auto">
                    <div class="form-check mb-2">
                        <input class="form-check-input" type="checkbox">
                        <label class="form-check-label" v-model="properties.isRecursive">
                            Recursive
                        </label>
                    </div>
                </div>
            </div>
            <div v-for="c in content" :key="c.id">
                <container v-if="c.type=='container'" :content="c.content" @selfDestroy="deleteFromContainer(c)" v-model="c.properties"/>
                <text-input v-else-if="c.type=='textInput'" v-model="c.name" @selfDestroy="deleteFromContainer(c)"/>
            </div>
            <span>
                <a class="btn btn-default" @click="addContainer"><folder-plus-outline /></a>
                <a class="btn btn-default" @click="addTextInput"><text-box-plus-outline /></a>
            </span>
            <span class="align-right">
                <a v-if="!isRoot" class="btn btn-light" @click="$emit('selfDestroy')"><delete class="light-button-content" /></a>
            </span>
        </div>
    </div>
</template>

<script>
import '../styles.css';
import FolderPlusOutline from 'vue-material-design-icons/FolderPlusOutline.vue';
import TextBoxPlusOutline from 'vue-material-design-icons/TextBoxPlusOutline.vue';
import Delete from 'vue-material-design-icons/Delete.vue';
import TextInput from './textInput.vue';
export default {
    props: {
        content: {
            type: Array,
            required: true
        },
        isRoot: {
            type: Boolean,
            default: false
        },
    },
    data() {
        return {
            properties: {
                description: '',
                isRecursive: false
            }
        };
    },
    methods: {
        updateProperties(){
            this.$emit('input', this.properties)
        },
        generateRandomId() {
            return Math.random().toString(36).substring(7)
        },
        addContainer() {
            this.content.push({
                type: 'container',
                content: [],
                properties: {},
                id: this.generateRandomId()
            })
        },
        addTextInput() {
            this.content.push({
                type: 'textInput',
                content: {
                    name:''
                },
                id: this.generateRandomId()
            })
        },
        deleteFromContainer(item) {
            if( item.type == 'container' &&
            item.content.length != 0 && !confirm("Are you sure?")) {
                return
            }

            this.content.splice(this.content.indexOf(item), 1);
        }
    },
    components: {
        FolderPlusOutline,
        TextBoxPlusOutline,
        Delete,
        container: () => import('./container'),
        TextInput
    }
}
</script>
