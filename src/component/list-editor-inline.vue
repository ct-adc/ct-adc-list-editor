<template>
    <ul class="list-group">
        <li class="list-group-item" v-if="hasHead">
            <div class="row">
                <slot name="head">
                    <div :class="firstGridClass">
                        <slot name="head-form">
    
                        </slot>
                    </div>
                    <div :class="secondGridClass">
                        <slot name="head-remove">
    
                        </slot>
                    </div>
                </slot>
            </div>
        </li>
        <template v-if="count > 0">
            <li class="list-group-item"
                v-for="n in count"
                :key="n - 1">
                <div class="row">
                    <slot name="list" :index="n-1">
                        <div :class="firstGridClass">
                            <slot name="list-form" :index="n - 1">
                                
                            </slot>
                        </div>
                        <div :class="secondGridClass">
                            <slot name="list-button" v-if="n > minCount" :index="n-1">
                                <button type="button" v-if="buttons.order"
                                    class="btn btn-sm btn-primary"
                                    :class="{disabled: !isItemUpOrderable(n-1)}"
                                    :disabled="!isItemUpOrderable(n-1)"
                                    @click="isItemUpOrderable(n-1) ? orderUp(n-1) : null">
                                    <span class="glyphicon glyphicon-arrow-up"></span> {{orderUpButtonText}}
                                </button>
                                <button type="button" v-if="buttons.order" 
                                    class="btn btn-sm btn-primary"
                                    :class="{disabled: !isItemDownOrderable(n-1)}"
                                    :disabled="!isItemDownOrderable(n-1)"
                                    @click="isItemDownOrderable(n-1) ? orderDown(n-1) : null">
                                    <span class="glyphicon glyphicon-arrow-down"></span> {{orderDownButtonText}}
                                </button>
                                <button type="button" v-if="buttons.remove" 
                                    class="btn btn-sm btn-danger"
                                    :class="{disabled: !isItemRemovable(n-1)}"
                                    :disabled="!isItemRemovable(n-1)"
                                    @click="isItemRemovable(n-1) ? remove(n-1) : null">
                                    <span class="glyphicon glyphicon-trash"></span> {{removeButtonText}}
                                </button>
                            </slot>
                        </div>
                    </slot>
                </div>
            </li>
        </template>
        <template v-else>
            <li class="list-group-item text-center text-muted">
                {{emptyText}}
            </li>
        </template>
        <li class="list-group-item text-center" v-if="addAble">
            <slot name="footer">
                <button type="button" class="btn btn-sm btn-info" @click="add">
                    <span class="glyphicon glyphicon-plus"></span> {{addButtonText}}
                </button>
            </slot>
        </li>
    </ul>
</template>

<script>
    import script from './script';
    
    export default {
        mixins: [script],
        props: {
            hasHead: {
                type: Boolean,
                default: true
            },
            grid: {
                type: Object,
                default(){
                    return {
                        lg: [9, 3],
                        sm: [8, 4],
                        xs: [8, 4]
                    };
                }
            }
        },
        computed: {
            firstGridClass(){
                return `col-lg-${this.grid.lg[0]} col-sm-${this.grid.sm[0]} col-xs-${this.grid.xs[0]}`;
            },
            secondGridClass(){
                return `col-lg-${this.grid.lg[1]} col-sm-${this.grid.sm[1]} col-xs-${this.grid.xs[1]}`;
            }
        }
    };
</script>


