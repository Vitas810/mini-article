<template>
    <button :style="`background-color: ${color};`">
        {{ text }}
        <plus />
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
            color: {
                type: String,
                require: false,
                default: '#ED5252'
            },
        }
    }
</script>

<style lang="scss">
    button {
        display: flex;
        align-items: center;
        gap: 8px;
        padding: 9px 16px 11px;
        border-radius: 3px;
        font-size: 16px;
        line-height: 24px;
        text-align: center;
        color: #FFFFFF;
        border: none;
        font-weight: 500;
    }
</style>