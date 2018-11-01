<template>
    <div>
        <list-editor :has-head="hasHead"
                     :initial-count="items.length"
                     :step="3"
                     :min-count="0"
                     :max-count="10"
                     add-button-text="新增定制"
                     remove-button-text="删除"
                     empty-text="为空定制"
                     :buttons="buttons"
                     :is-removable="isRemovable"
                     :is-orderable="isOrderable"
                     @add="add"
                     @remove="remove"
                     @order-up="orderUp"
                     @order-down="orderDown">
            <template slot="head-form">
                <div class="col-sm-4 col-xs-4">
                    <i class="red">*</i> <b>条件</b> <span class="text-muted">(只能填入数字)</span>
                </div>
                <div class="col-sm-4 col-xs-4">
                    <i class="red">*</i> <b>操作符</b>
                </div>
                <div class="col-sm-4 col-xs-4">
                    <i class="red">*</i> <b>值</b>
                </div>
            </template>
            <template slot="head-remove">
                操作
            </template>
            <template slot="list-form"
                      slot-scope="{index}">
                <div :key="index">
                    <div class="col-sm-4 col-xs-4">
                        <select class="form-control"
                                v-model="items[index].a">
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                        </select>
                    </div>
                    <div class="col-sm-4 col-xs-4">
                        <select class="form-control"
                                v-model="items[index].b">
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                        </select>
                    </div>
                    <div class="col-sm-4 col-xs-4">
                        <select class="form-control"
                                v-model="items[index].c">
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                        </select>
                    </div>
                </div>
            </template>
        </list-editor>
    </div>
</template>
<script>
import {Inline as ListEditor} from 'index.js';
export default {
    components: {
        ListEditor
    },
    data(){
        return {
            hasHead: true,
            buttons: {
                order: true,
                remove: true
            },
            items: [{
                a: 1,
                b: 2,
                c: 3,
                removable: true
            }, {
                a: 3,
                b: 2,
                c: 1,
                removable: false
            }]
        };
    },
    // computed: {
    //     isRemovable(){
    //         return this.items.map(item=>{
    //             return item.removable;
    //         });
    //     }
    // },
    methods: {
        isRemovable(index){
            return this.items[index].a === 1;
        },
        isOrderable(index){
            return this.items[index].a === 1;
        },
        add(count){
            const toAddList = new Array(count).fill('').map(()=>{
                return {
                    a: 1,
                    b: 1,
                    c: 1,
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
