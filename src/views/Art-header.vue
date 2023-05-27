<template>
    <div class="header">
        <btn text="Создать категорию"></btn>
        <div class="header-search">
            <input type="text" placeholder="Найти статью">
            <search />
        </div>
    </div>
</template>

<script>
    document.title = 'article-page';
    import btn from '@/components/btn.vue';
    import search from '@/assets/svg/search.svg'
    export default {
        name: 'Article-header',
        components: {
            btn,
            search
        }
        }
</script>
<style lang="scss">
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 16px;
        &-search {
            display: flex;
            align-items: center;
            flex-grow: 1;
            background: #FFFFFF;
            border: 1px solid #D9DDE6;
            border-radius: 4px;
            & input {
                padding: 11px 0 13px 16px;
                width: calc(100% - 35px);
                border: none;
                font-family: 'Montserrat';
                font-style: normal;
                font-weight: 500;
                font-size: 14px;
                line-height: 22px;
                &::placeholder {
                    display: flex;
                    align-items: center;
                    color: #A0A6BF;
                }
            }
            & svg {
                margin-right: 11px;
            }
        }
    }
</style>