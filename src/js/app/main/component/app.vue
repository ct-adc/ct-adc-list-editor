<template>
    <div class="container-fluid">
        <ul class="nav nav-tabs">
            <li role="presentation" :class="{active: index === 0}" @click="toggle(0)">
                <a href="#">
                    块状列表编辑
                </a>
            </li>
            <li role="presentation" :class="{active: index === 1}" @click="toggle(1)">
                <a href="#">
                    行内列表编辑
                </a>
            </li>
        </ul>
        <div class="mt20">
            <block v-show="index === 0"></block>
            <inline v-show="index === 1"></inline>
        </div>
    </div>
</template>
<script>
import Block from './block';
import Inline from './inline';
export default {
    components: {
        Block,
        Inline
    },
    data(){
        return {
            index: 0
        };
    },
    methods: {
        toggle(index){
            this.index = index;
        }
    }
};
</script>
