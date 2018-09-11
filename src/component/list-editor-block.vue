<template>
    <div class="mt20">
        <slot name="list" v-if="count > 0">
            <div v-for="n in count" :key="n - 1">
                <div class="panel-heading mt20 pl20 pr20">
                    <span class="glyphicon glyphicon-chevron-down pointer mr10"
                        style="line-height:14px;"
                        :class="visible[n-1] ? '' : 'overturn'"
                        @click="toggle(n-1)">
                    </span>
                    <slot name="list-head" :index="n-1">
                        <slot name="list-head-title" :index="n-1">
                            ({{n}})
                        </slot>
                        <span class="pull-right">
                            <slot name="list-head-remove" :index="n-1">
                                <button type="button" 
                                    class="btn btn-xs btn-danger" 
                                    :class="{disabled: isRemovable(n-1)}"
                                    :disabled="isRemovable(n-1)" 
                                    @click="isRemovable(n-1) ? remove(n-1) : null">
                                    删除
                                </button>
                            </slot>
                        </span>
                    </slot>
                </div>
                <transition v-on:enter="enter" v-on:leave="leave">
                    <div v-show="visible[n-1]" style="overflow:hidden;">
                        <slot name="list-body" :index="n-1">

                        </slot>
                    </div>
                </transition>
            </div>
        </slot>
        <div class="text-muted f14" style="height: 200px;line-height:200px;text-align:center;" v-if="count === 0">
            {{emptyText}}
        </div>
        <hr style="border-top-style: dashed">
        <div class="mt20 text-center">
            <button type="button" class="btn btn-sm btn-info" v-if="addAble" @click="add">
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
                default() {
                    return [];
                }
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
                el.style.visible = 'invisible';
                el.style.height = 'auto';
                const height = el.clientHeight;

                el.style.visible = 'visibile';
                el.style.height = 0;
                Velocity(el, {
                    height: `${height}px`
                }, {
                    duration: this.duration,
                    complete: function() {
                        el.style.height = 'auto';
                        done();
                    }
                });
            },
            leave: function(el, done) {
                const height = el.clientHeight;

                el.style.height = height + 'px';
                Velocity(el, {
                    height: 0
                }, {
                    duration: this.duration,
                    complete: done
                });
            },
            // 事件
            toggle(index) {
                this.$emit('toggle', index);
            }
        }
    };
</script>

<style scoped>
    .panel-heading {
        background: #f5f5f5
    }
    
    .overturn {
        transform-origin: center center;
        transform: rotate(-90deg);
        transition: transform 0.5s;
    }
    
    .pointer {
        cursor: pointer;
    }
</style>
