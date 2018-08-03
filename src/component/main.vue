<template>
    <component :is="component"></component>
</template>

<script>
import ListEditorInline from './list-editor-inline';
import ListEditorBlock from './list-editor-block';

export default {
    components: {
        ListEditorInline,
        ListEditorBlock
    },
    props: {
        title: {
            type: String,
            default: ''
        },
        emptyText: {
            type: String,
            default: ''
        },
        buttonText: {
            type: String,
            default: ''
        },
        isEmpty: {
            type: Boolean,
            default: false
        },
        initialCount: {
            type: Number,
            default: 0
        },
        maxCount: {
            type: Number,
            default: -1
        },
        step: {
            type: Number,
            default: 1
        },
        minCount: {
            type: Number,
            default: 0
        }
    },
    data(){
        return {
            count: Math.max(this.initialCount, this.minCount)
        };
    },
    computed: {
        addAble(){
            return this.maxCount === -1 || this.count < this.maxCount;
        },
        component(){
            return {
                inline: 'ListEditorInline',
                block: 'ListEditorBlock'
            }[this.type];
        }
    },
    methods: {
        removeItem(index){
            this.count = this.count - 1;
            this.$emit('remove', index);
        },
        addItem(){
            if (this.maxCount !== -1 && this.count + this.step >= this.maxCount){
                this.count = this.maxCount;   
            } else {
                this.count = this.count + this.step;
            }
            this.$emit('add', this.step);
        }
    },
    watch: {
        initialCount(){
            this.count = Math.max(this.initialCount, this.minCount);
        },
        minCount(){
            this.count = Math.max(this.initialCount, this.minCount);
        }
    }
};
</script>

