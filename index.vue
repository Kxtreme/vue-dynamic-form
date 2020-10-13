<template>
    <container :content="baseContent.content" :languages="languages" :selectedLanguage="selectedLanguage" :isRoot="true"/>
</template>
<script>
require('bootstrap')
import Utils from './utils.js';
import container from './components/container.vue'
export default {
    props: {
        content: {
            type: Array,
            required: true
        },

        languageKey: {
            type: String,
            default: 'language'
        },
        selectedLanguage: {
            type: String,
            default: 'en'
        },
        languageValue: {
            type: String,
            default: 'form'
        }
    },
    data() {
        return {
            baseContent: {
                content: []
            }
        };
    },
    methods: {
        reDo() {
            this.populateLanguages();
            this.generateBaseContent();
        },
        populateLanguages() {
            this.content.forEach(c => {
                if(typeof c != 'object') return
                if(typeof Array.isArray(c[this.languageValue])) return
                c[this.languageValue] = []
            });
        },
        generateBaseContent() {
            const id = Utils.generateRandomId()
            const properties  = {}
            this.baseContent = {
                type: 'container',
                content: [],
                properties,
                id
            }
        }
    },
    components: {
        container
    },
    computed: {
        languages: function () {
            return Object.keys(this.structuredContent);
        },

        structuredContent: function () {
            const content = this.content.reduce((acc, cur) => {
                acc[cur[this.languageKey]] = cur[this.languageValue]
                return acc;
            }, {})
            if(Object.keys(content).length == 0) {
                content['en'] = this.content
            }
            return content;
        }
    },
    watch: {
        content: function () {
            this.reDo()
        }
    },
    mounted() {
        this.reDo()
    }
}
</script>
