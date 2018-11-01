<template>
    <div>
        <list-editor :initial-count="2"
                     :step="3"
                     :min-count="0"
                     :max-count="10"
                     add-button-text="新增定制"
                     remove-button-text="删除定制"
                     empty-text="为空定制"
                     :buttons="buttons"
                     :visible="visible"
                     :is-removable="isRemovable"
                     @add="add"
                     @remove="remove"
                     @toggle="toggle"
                     @order-up="orderUp"
                     @order-down="orderDown">
            <span slot="list-head-title"
                  slot-scope="{index}">
                ({{index + 1}}) 标题定制
            </span>
            <div slot="list-body"
                 slot-scope="{index}">
                <div class="p20">
                    <input type="text"
                           class="form-control"
                           v-model="items[index].name">
                    <input type="text"
                           class="form-control mt20"
                           v-model="items[index].value">
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
            buttons: {
                order: false,
                remove: true
            },
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
        }
        // isRemovable(){
        //     return this.items.map(item=>{
        //         return item.removable;
        //     });
        // }
    },
    methods: {
        isRemovable(index){
            return index === 1;
        },
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
        },
        orderUp(index){
            const itemsClone = JSON.parse(JSON.stringify(this.items));
            const toUp = JSON.parse(JSON.stringify(itemsClone[index]));
            
            itemsClone[index] = JSON.parse(JSON.stringify(itemsClone[index - 1]));
            itemsClone[index - 1] = toUp;
            this.items = itemsClone;
        },
        orderDown(index){
            const itemsClone = JSON.parse(JSON.stringify(this.items));
            const toDown = JSON.parse(JSON.stringify(itemsClone[index]));
            
            itemsClone[index] = JSON.parse(JSON.stringify(itemsClone[index + 1]));
            itemsClone[index + 1] = toDown;
            this.items = itemsClone;
        }
    }
};
</script>
