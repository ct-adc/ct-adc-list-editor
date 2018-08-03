<template>
    <ul class="list-group">
        <li class="list-group-item">
            <div class="row">
                <slot name="title">
                    <div class="col-sm-11 col-xs-10">
                        <slot name="title-form">
                            
                        </slot>
                    </div>
                    <div class="col-sm-1 col-xs-2">
                        <slot name="title-remove">
                            
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
                        <div class="col-sm-11 col-xs-10">
                            <slot name="list-form" :index="n - 1">
                                
                            </slot>
                        </div>
                        <div class="col-sm-1 col-xs-2">
                            <slot name="list-remove" v-if="n > minCount" :index="n-1">
                                <button type="button" 
                                    class="btn btn-sm btn-danger pull-right"
                                    :class="{disabled: !removable[n-1]}"
                                    :disabled="!removable[n-1]"
                                    @click="removable[n-1] ? remove(n-1) : null">
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
        <slot name="bottom">
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
    mixins: [script]
};
</script>


