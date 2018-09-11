<script>
export default {
    props: {
        // 删除按钮的文字
        removeButtonText: {
            type: String,
            default: '删除'
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
        removable: {
            type: Array,
            default(){
                return [];
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
        isRemovable(index){
            return typeof this.removable[index] === 'undefined' || this.removable[index];
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
            if (typeof this.removable[index] === 'undefined' || this.removable[index]){
                this.count = this.count - 1;
                this.$emit('remove', index);
                return true;
            }
            return false;
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
