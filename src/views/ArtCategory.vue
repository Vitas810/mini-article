<template>
    <section class="art-category">
        <h2 class="art-category__title">
            Название категории
            <sup>(4)</sup>
        </h2>
        <div class="art-category__arrow">
            <chevron-up />
            <menu-cat class="js-popup-edite" />
        </div>
        <div class="art-category__items">
            <card />
            <card />
        </div>

        <div class="art-category-popup"
             v-cloak
             v-show="showModalMenuEdite"
        >
            <ul class="art-category-popup__list">
                <li>
                    <button type="button" @click="editeCategory">Редактировать</button>
                </li>
                <li><button type="button">Удалить</button></li>
            </ul>
        </div>

        <art-create-category :show-popup-category="showPopupEditeCategory"
                            title-popup="Редактирование категории"
                            name-category-popup="Название категории"
                            parent-category-popup="Родительская категория 1"
                            @close_popup="closePopup"
        />
    </section>
</template>

<script>
    import card from '@/components/card.vue';
    import chevronUp from '@/assets/svg/chevron-up.svg';
    import menuCat from '@/assets/svg/menu.svg';
    import ArtCreateCategory from '@/views/CreateCategory.vue'; 

    export default {
        name: 'ArtCategory',
        components: {
            card,
            chevronUp,
            menuCat,
            ArtCreateCategory
        },
        created() {
            document.addEventListener('click', e => {
                let menu = document.querySelector('.js-popup-edite');
                let target = e.target;
                let isMenu = target === menu || menu?.contains(target);

                if (menu?.contains(target)) {
                    this.showModalMenuEdite = true;
                }
                if (!isMenu && this.showModalMenuEdite) {
                    this.showModalMenuEdite = false;
                }
            });
        },
        data() {
            return {
                showModalMenuEdite: false,
                showPopupEditeCategory: false
            }
        },
        methods: {
            editeCategory() {
                this.showPopupEditeCategory = true;
            },
            closePopup(val) {
                this.showPopupEditeCategory = val;
            }
        }
    }
</script>

<style lang="scss">
    .art {
        &-category {
            position: relative;
            &__title {
                margin-top: 48px;
                margin-bottom: 16px;
                font-weight: 500;
                font-size: 24px;
                line-height: 32px;
                color: #303446;
                & > sup {
                    font-weight: 600;
                    font-size: 16px;
                    line-height: 24px;
                    color: #A0A6BF;
                }
            }
            &__arrow {
                position: absolute;
                right: 0;
                top: 0;
                display: flex;
                gap: 16px;
                & svg {
                    cursor: pointer;
                }
            }
            &__items {
                display: flex;
                gap: 24px;
                flex-wrap: wrap;
            }
            &-popup {
                background: #fff;
                padding: 8px 9px;
                box-shadow: 0px 10px 40px rgba(0, 0, 0, 0.07);
                border-radius: 5px;
                width: fit-content;
                position: absolute;
                top: 30px;
                right: 20px;
                &__list {
                    padding-left: 0;
                    margin: 0;
                    & li {
                        list-style-type: none;
                        font-weight: 500;
                        font-size: 14px;
                        line-height: 22px;
                        color: #4D5163;
                        padding: 6px 8px;
                        cursor: pointer;
                        &:hover {
                            background: rgba(48, 52, 70, 0.03);
                            border-radius: 5px;
                        }

                        & button {
                            border: none;
                            background: transparent;
                            cursor: pointer;
                        }
                    }
                }
            }
        }
    }
</style>