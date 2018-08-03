<script>
export default {
    props: {
        removeButtonText: {
            type: String,
            default: '删除'
        },
        // 新增按钮的文字
        addButtonText: {
            type: String,
            default: '新增'
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
            default: ''
        },
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
        addAble(){
            return this.maxCount === -1 || this.count < this.maxCount;
        }
    },
    methods: {
        add(){
            if (this.maxCount !== -1 && this.count + this.step >= this.maxCount){
                this.count = this.maxCount;   
            } else {
                this.count = this.count + this.step;
            }
            this.$emit('add', this.step);
        },
        remove(index){
            this.count = this.count - 1;
            this.$emit('remove', index);
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
