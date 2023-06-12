<template>
    <button @click="clickBtn">
        {{ text }}
        <plus v-if="showIcon" />
     </button>
</template>

<script>
    import plus from '../assets/svg/plus.svg';

    export default {
        name: 'Art-btn',
        components: {
            plus
        },
        props: {
            text: {
                type: String,
                require: true
            },
            showIcon: {
                type: Boolean,
                require: false,
                default: true
            }
        },
        data() {
            return {}
        },
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
        padding: 10px 16px 12px;
        border-radius: 3px;
        font-size: 16px;
        line-height: 24px;
        text-align: center;
        color: #FFFFFF;
        border: none;
        font-weight: 500;
        cursor: pointer;
        background-color: #ED5252;
        &:hover {
            background-color: #F06C6C;
        }
        &:active {
            background-color: #D54A4A;
        }
    }
</style>