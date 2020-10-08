<template>
    <div>
        <div class="alert alert-info">
            <div v-for="c in content" :key="c.id">
                <container v-if="c.type=='container'" :content="c.content" @selfDestroy="deleteFromContainer(c)"/>
                <text-input v-else-if="c.type=='textInput'" v-model="c.name" @selfDestroy="deleteFromContainer(c)"/>
            </div>
            <span class="left-icons">
                <a class="btn btn-default" @click="addContainer"><folder-plus-outline /></a>
                <a class="btn btn-default" @click="addTextInput"><text-box-plus-outline /></a>
            </span>
            <span class="right-icons">
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
