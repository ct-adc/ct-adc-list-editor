<template>
    <div>
        <list-editor :initial-count="items.length" 
            :step="3" 
            :min-count="0"
            :max-count="10" 
            add-button-text="新增定制" 
            remove-button-text="删除定制"
            :removable="removable" 
            empty-text="为空定制" 
            @add="add" 
            @remove="remove">
            <template slot="title-form">
                <div class="col-sm-4">
                    <i class="red">*</i> <b>条件</b> <span class="text-muted">(只能填入数字)</span>
                </div>
                <div class="col-sm-4">
                    <i class="red">*</i> <b>操作符</b>
                </div>
                <div class="col-sm-4">
                    <i class="red">*</i> <b>值</b>
                </div>
            </template>
            <template slot="list-form" slot-scope="{index}">
                <div class="col-sm-4">
                    <select class="form-control" :key="index"></select>
                </div>
                <div class="col-sm-4">
                    <select class="form-control" :key="index"></select>
                </div>
                <div class="col-sm-4">
                    <select class="form-control" :key="index"></select>
                </div>
            </template>
        </list-editor>
    </div>
</template>
<script>
import ListEditor from 'list-editor-inline';
export default {
    components: {
        ListEditor
    },
    data(){
        return {
            items: [{
                name: 'a1',
                value: 'b1',
                visible: true,
                removable: true
            }, {
                name: 'a2',
                value: 'b2',
                visible: true,
                removable: false
            }]
        };
    },
    computed: {
        removable(){
            return this.items.map(item=>{
                return item.removable;
            });
        }
    },
    methods: {
        add(count){
            const toAddList = new Array(count).fill('').map(()=>{
                return {
                    name: '',
                    value: '',
                    visible: true,
                    removable: true
                };
            });

            this.items = this.items.concat(toAddList);
        },
        remove(index){
            this.items.splice(index, 1);
        }
    }
};
</script>
