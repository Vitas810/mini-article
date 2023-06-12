<template>
    <header class="header">
        <btn text="Создать категорию" @click="showCreateCategory"/> 
        <div class="header-search">
            <input type="text" placeholder="Найти статью">
            <search />
        </div>

        <art-create-category :show-popup-category="showPopupCategory"
                            @close_popup="closePopup"
        />
    </header>
</template>

<script>
    document.title = 'article-page';
    import btn from '@/components/btn.vue';
    import search from '@/assets/svg/search.svg';
    import ArtCreateCategory from '@/views/CreateCategory.vue';

    export default {
        name: 'ArtHeader',
        components: {
            btn,
            search,
            ArtCreateCategory
        },
        data() {
            return {
                showPopupCategory: false
            }
        },
        methods: {
            showCreateCategory() {
                this.showPopupCategory = true;
            },
            closePopup(value) {
                this.showPopupCategory = value;
            }
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
                    &:focus {
                        color: #303446;
                    }
                }
                &:focus {
                    outline:1px solid #BFC3D5;
                    color: #303446;
                }
            }
            & svg {
                margin-right: 11px;
            }
        }
    }
</style>