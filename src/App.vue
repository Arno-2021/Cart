<template>
    <div class="app">
        <MyHeader title="购物车案例"></MyHeader>
        <Goods
            :goods="item"
            v-for="item in list"
            :key="item.id"
            @changeVal="changeValFn"
            @changeCount="changeCountFn"
        ></Goods>
        <MyFooter :list="list" @switchAll="switchAllFn"></MyFooter>
    </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyFooter from './components/MyFooter.vue'
import Goods from './components/Goods.vue'
import axios from 'axios'
export default {
    data() {
        return {
            list: [],
        }
    },
    components: {
        MyHeader,
        MyFooter,
        Goods,
    },
    methods: {
        changeValFn(id) {
            const res = this.list.find(item => item.id === id)
            res.goods_state = !res.goods_state
        },
        switchAllFn(value) {
            this.list.forEach(item => (item.goods_state = value))
        },
        changeCountFn(value, id) {
            this.list.find(item => item.id === id).goods_count = value
        },
    },
    async created() {
        const res = await axios({
            method: 'get',
            url: 'https://www.escook.cn/api/cart',
        })
        const { status, list } = res.data
        if (status === 200) {
            this.list = list
        }
    },
}
</script>

<style scoped>
.app {
    padding-top: 45px;
    padding-bottom: 50px;
}
</style>
