<template>
    <div>
        <list-editor :initial-count="2" 
            :step="3" 
            :min-count="0"
            :max-count="10" 
            add-button-text="新增定制" 
            remove-button-text="删除定制" 
            empty-text="为空定制" 
            :visible="visible"
            :removable="removable"
            @add="add" 
            @remove="remove"
            @toggle="toggle">
            <span slot="list-head-title" slot-scope="{index}">
                ({{index + 1}}) 标题定制
            </span>
            <div slot="list-body" 
                slot-scope="{index}" 
                v-show="items[index].visible" 
                style="maxHeight: 200px;overflow:hidden;">
                <div class="p20">
                    <input type="text" class="form-control" v-model="items[index].name">
                    <input type="text" class="form-control mt20" v-model="items[index].value">
                </div>
            </div>
        </list-editor>
    </div>
</template>
<script>
import {Block as ListEditor} from 'index.js';
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
        visible(){
            return this.items.map(item=>{
                return item.visible;
            });
        },
        removable(){
            return this.items.map(item=>{
                return item.removable;
            });
        }
    },
    methods: {
        toggle(index){
            this.items.map((item, i)=>{
                if (i === index){
                    item.visible = !item.visible;
                }
                return item;
            });
        },
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
