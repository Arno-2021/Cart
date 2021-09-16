<template>
    <div class="my-counter">
        <button type="button" class="btn btn-light" @click="miner">-</button>
        <input
            type="number"
            class="form-control inp"
            :value="count"
            @change="changeCount"
        />
        <button type="button" class="btn btn-light" @click="plus">+</button>
    </div>
</template>

<script>
export default {
    props: {
        count: {
            type: Number,
            require: true,
        },
    },
    methods: {
        changeCount(e) {
            let num = +e.target.value
            if (num < 1) {
                num = 1
                this.$forceUpdate();
            }
            this.$emit('changeCount', num)
        },
        plus() {
            this.$emit('changeCount', this.count + 1)
        },
        miner() {
            if (this.count === 1) {
                return
            }
            this.$emit('changeCount', this.count - 1)
        },
    },
}
</script>

<style lang="less" scoped>
.my-counter {
    display: flex;
    .inp {
        width: 45px;
        text-align: center;
        margin: 0 10px;
    }
}
</style>
