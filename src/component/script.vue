<script>
export default {
    props: {
        // 删除按钮的文字
        removeButtonText: {
            type: String,
            default: '删除'
        },
        orderUpButtonText: {
            type: String,
            default: '上移'
        },
        orderDownButtonText: {
            type: String,
            default: '下移'
        },
        // 新增按钮的文字
        addButtonText: {
            type: String,
            default: '添加'
        },
        // 允许的最小数量
        minCount: {
            type: Number,
            default: 0
        },
        // 允许的最大数量
        maxCount: {
            type: Number,
            default: -1
        },
        // 起始数量
        initialCount: {
            type: Number,
            default: 0
        },
        // 增加步长(即点击一次增加按钮可以增加几个)
        step: {
            type: Number,
            default: 1
        },
        // 为空时显示的内容
        emptyText: {
            type: String,
            default: '暂无数据'
        },
        // 每项是否可删除
        isRemovable: {
            type: [Array, Object, Function],
            default(){
                return ()=>true;
            }
        },
        // 检测一项是否可调整排序
        isOrderable: {
            type: [Array, Object, Function],
            default(){
                return ()=>true;
            }
        },
        buttons: {
            type: Object,
            default(){
                return {
                    order: true,
                    remove: true
                };
            }
        }
    },
    data(){
        return {
            count: Math.max(this.initialCount, this.minCount)
        };
    },
    computed: {
        /**
         * 是否可继续添加项目
         */
        addAble(){
            return this.maxCount === -1 || this.count < this.maxCount;
        }
    },
    methods: {
        isItemRemovable(index){
            if (Array.isArray(this.isRemovable) || typeof this.isRemovable === 'object'){
                return this.isRemovable[index];
            }
            if (typeof this.isRemovable === 'function'){
                return this.isRemovable(index);
            }
            return true;
        },
        $_isItemOrderable(index){
            if (Array.isArray(this.isOrderable) || typeof this.isOrderable === 'object'){
                return this.isOrderable[index];
            }
            if (typeof this.isOrderable === 'function'){
                return this.isOrderable(index);
            }
            return true;
        },
        isItemUpOrderable(index){
            return index > 0 && this.$_isItemOrderable(index);
        },
        isItemDownOrderable(index){
            return index < this.count - 1 && this.$_isItemOrderable(index);
        },
        add(){
            const isMaxLimited = this.maxCount !== -1;
            const addToLimit = this.count + this.step >= this.maxCount;

            if (isMaxLimited && addToLimit){
                this.count = this.maxCount;   
            } else {
                this.count = this.count + this.step;
            }
            this.$emit('add', this.step);
        },
        /**
         * 删除项目
         */
        remove(index){
            console.log(this.isItemRemovable(index));
            if (this.isItemRemovable(index)){
                this.count = this.count - 1;
                this.$emit('remove', index);
                return true;
            }
            return false;
        },
        orderUp(index){
            this.$emit('order-up', index);
        },
        orderDown(index){
            this.$emit('order-down', index);
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
