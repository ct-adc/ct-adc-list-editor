<template>
    <div class="mt20">
        <slot name="list" v-if="count > 0">
            <div v-for="n in count"
                :key="n - 1">
                <div class="panel-heading mt20" style="background:#f5f5f5">
                    <slot name="list-head" :index="n-1">
                        <slot name="list-head-title" :index="n-1">
                            ({{n}})
                        </slot>
                        <span class="pull-right">
                            <a class="pointer" 
                                :class="removable[n-1] ? 'text-danger' : 'text-muted'" 
                                @click="removable[n-1] ? remove(n-1) : null">删除</a>
                            <span class="glyphicon glyphicon-chevron-down ml20 pointer"
                                :class="visible[n-1] ? '' : 'overturn'"
                                @click="toggle(n-1)"></span>
                        </span>
                    </slot>
                </div>
                <transition v-on:enter="enter"
                    v-on:leave="leave">
                    <slot name="list-body" :index="n-1">
                        
                    </slot>
                </transition>
            </div>
        </slot>
        <div class="text-muted f14" 
            style="height: 200px;line-height:200px;text-align:center;" 
            v-if="count === 0">
            {{emptyText}}
        </div>
        <hr style="border-top-style: dashed">
        <div class="mt20 text-center">
            <button type="button" 
                class="btn btn-sm btn-info"
                v-if="addAble"
                @click="add">
                <span class="glyphicon glyphicon-plus"></span> {{addButtonText}}
            </button>
        </div>
    </div>
</template>
<script>
import script from './script';
import Velocity from 'velocity-animate';

export default {
    mixins: [script],
    props: {
        // 列表的可见状态
        visible: {
            type: Array,
            default(){
                return [];
            }
        },
        // 内容区域的最大高度
        maxHeight: {
            type: Number,
            default: 200
        },
        // 动画持续时长 单位 ms
        duration: {
            type: Number,
            default: 500
        }
    },
    methods: {
        // 动画
        enter: function(el, done) {
            Velocity(el, { maxHeight: `${this.maxHeight}px` }, { duration: this.duration }, { complete: done });
        },
        leave: function(el, done) {
            Velocity(el, { maxHeight: 0 }, { duration: this.duration }, { complete: done });
        },
        // 事件
        toggle(index){
            this.$emit('toggle', index);
        }
    }
};
</script>
<style scoped>
.overturn{
    transform-origin: center center;
    transform: rotate(180deg);
    transition: transform 0.5s;
}
.pointer{
    cursor: pointer;
}
</style>
