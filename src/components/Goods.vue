<template>
    <div class="my-goods-item">
        <div class="left">
            <div class="custom-control custom-checkbox">
                <input
                    type="checkbox"
                    class="custom-control-input"
                    :id="goods.id"
                    :checked="goods.goods_state"
                    @change="changeFn"
                />
                <label class="custom-control-label" :for="goods.id">
                    <img :src="goods.goods_img" alt="" />
                </label>
            </div>
        </div>
        <div class="right">
            <div class="top">{{ goods.goods_name }}</div>
            <div class="bottom">
                <span class="price">¥{{ goods.goods_price }}</span>
                <span
                    ><MyCount
                        :count="goods.goods_count"
                        @changeCount="changeCountFn"
                    ></MyCount
                ></span>
            </div>
        </div>
    </div>
</template>

<script>
import MyCount from './MyCount.vue'
export default {
    components: {
        MyCount,
    },
    props: {
        goods: {
            type: Object,
            require: true,
        },
    },
    methods: {
        changeFn() {
            this.$emit('changeVal', this.goods.id)
        },
        changeCountFn(num) {
            this.$emit('changeCount', num, this.goods.id)
        },
    },
}
</script>

<style lang="less" scoped>
.my-goods-item {
    display: flex;
    padding: 10px;
    border-bottom: 1px solid #ccc;
    .left {
        img {
            width: 120px;
            height: 120px;
            margin-right: 8px;
            border-radius: 10px;
        }
        .custom-control-label::before,
        .custom-control-label::after {
            top: 50px;
        }
    }
    .right {
        flex: 1;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        .bottom {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            .price {
                color: red;
                font-weight: bold;
            }
        }
    }
}
</style>
