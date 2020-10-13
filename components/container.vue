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
                <container v-if="c.type=='container'" :content="c.content" :languages="languages" :selectedLanguage="selectedLanguage" @selfDestroy="deleteFromContainer(c)" v-model="c.properties"/>
                <text-input v-else-if="c.type=='textInput'" :content="c.content" :languages="languages" :selectedLanguage="selectedLanguage" @selfDestroy="deleteFromContainer(c)"/>
                <select-input v-else-if="c.type=='select'" :content="c.content" :languages="languages" :selectedLanguage="selectedLanguage" v-model="c.properties" @selfDestroy="deleteFromContainer(c)"/>
            </div>
            <span>
                <a class="btn btn-default" @click="addContainer"><folder-plus-outline /></a>
                <a class="btn btn-default" @click="addTextInput"><text-box-plus-outline /></a>
                <a class="btn btn-default" @click="addSelect"><playlist-plus /></a>
            </span>
            <span class="align-right">
                <a v-if="!isRoot" class="btn btn-light" @click="$emit('selfDestroy')"><delete class="light-button-content" /></a>
            </span>
        </div>
    </div>
</template>

<script>
import '../styles.css';
import Utils from '../utils.js';
import FolderPlusOutline from 'vue-material-design-icons/FolderPlusOutline.vue';
import TextBoxPlusOutline from 'vue-material-design-icons/TextBoxPlusOutline.vue';
import PlaylistPlus from 'vue-material-design-icons/PlaylistPlus.vue';
import Delete from 'vue-material-design-icons/Delete.vue';
import TextInput from './textInput.vue';
import SelectInput from './select.vue';
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
            type: Array,
            required: true
        },
        isRoot: {
            type: Boolean,
            default: false
        }
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

        addContainer() {
            this.content.push({
                type: 'container',
                content: [],
                properties: {},
                id: Utils.generateRandomId()
            })
        },
        addTextInput() {
            this.content.push({
                type: 'textInput',
                content: this.languages.reduce((acc, cur) => {
                    acc[cur] = ''
                    return acc;
                }, {}),
                id: Utils.generateRandomId()
            })
        },
        addSelect() {
            this.content.push({
                type: 'select',
                content: [],
                properties: {},
                id: Utils.generateRandomId()
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
        PlaylistPlus,
        container: () => import('./container'),
        TextInput,
        SelectInput
    }
}
</script>
