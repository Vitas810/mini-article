<template>
    <div class="header">
        <btn text="Создать категорию" /> 
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
        name: 'ArtHeader',
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
            &:hover {
                border: 1px solid #BFC3D5;
            }
            & input {
                padding: 11px 0 13px 16px;
                width: calc(100% - 35px);
                border: none;
                font-family: 'Montserrat';
                font-style: normal;
                font-weight: 500;
                font-size: 14px;
                line-height: 22px;
                cursor: pointer;
                &::placeholder {
                    display: flex;
                    align-items: center;
                    color: #A0A6BF;
                    &::focus {
                        color: #303446;
                    }
                }
                &:focus {
                    outline:   #BFC3D5;
                    color: #303446;
                }
            }
            & svg {
                margin-right: 11px;
            }
        }
    }
</style>