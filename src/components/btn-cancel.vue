<template>
    <button type="button" @click="clickBtn">Отмена</button>
</template>

<script>
    export default {
        name: 'Art-btn',
        methods: {
            clickBtn() {
                this.$emit('click');
            }
        }
    }
</script>

<style lang="scss" scoped>
    button {
        display: flex;
        align-items: center;
        gap: 8px;
        font-family: 'Montserrat';
        padding: 10px 16px;
        border-radius: 5px;
        font-size: 16px;
        line-height: 24px;
        text-align: center;
        color: #303446;
        border: none;
        font-weight: 500;
        cursor: pointer;
        background: rgba(10, 14, 32, 0.07);
        backdrop-filter: blur(10px);
        &:hover {
            background: rgba(10, 14, 32, 0.1);
        }
        &:active {
            background: rgba(10, 14, 32, 0.15);
        }
    }
</style>