<template>
    <section ref="modalCategory" class="category js-popup" v-if="showModal">
        <div class="category-modal">
            <h2 class="category__title">{{ title }}</h2>

            <form class="category-form">
                <label>
                    <input name="nameCreateCategory"
                            v-model="defaultCategory.name"
                            class="category__name"
                            type="text"
                            placeholder="Название" />
                </label>

                <art-select title="Родительская карточка (необязательно)"
                    :options="categoryList"
                    v-model="defaultCategory.parentCategory" />
                <art-select title="Вложенные статьи"
                    :options="parentCategories"
                    v-model="defaultCategory.nestedCategory" />

                <div class="category-footer">
                    <btn text="Сохранить" :showIcon="false"
                        @click="createCategory"
                    />
                    <btn-cancel @click="closePopup" />
                </div>
            </form>
        </div>
    </section>
</template>

<script>
    import btn from "@/components/btn.vue";
    import btnCancel from "@/components/btn-cancel.vue";
    import ArtSelect from "@/components/art-select.vue";

    export default {
        name: "ArtCreateCategory",
        props: {
            showPopupCategory: {
                type: Boolean,
            },
            titlePopup: {
                type: String,
                require: false,
                default: 'Новая категория'
            },
            nameCategoryPopup: {
                type: String,
                require: false,
                default: null
            },
            parentCategoryPopup: {
                type: String,
                require: false,
                default: null
            },
            nestedCategoryPopup: {
                type: String,
                require: false,
                default: null
            },
            editCategory: {
                type: Boolean,
                require: false,
                default: false
            }
        },
        components: {
            btn,
            btnCancel,
            ArtSelect,
        },
        created() {
            document.addEventListener('click', e => {
                let popup = document.querySelector('.js-popup');
                let target = e.target;
   
                if (popup == target) {
                    this.showModal = false;
                    this.$emit('close_popup', this.showModal);
                }
            });
        },
        data() {
            return {
                showModal: this.showPopupCategory || false,
                title: this.titlePopup || '',
                defaultCategory: {
                    name: this.nameCategoryPopup || '',
                    parentCategory: this.parentCategoryPopup || '',
                    nestedCategory: '',
                },
                parentCategories: [
                    { id: 1, name: 'Родительская категория 1'},
                    { id: 2, name: 'Родительская категория 2'},
                    { id: 3, name: 'Родительская категория 3'},
                    { id: 4, name: 'Родительская категория 4'},
                    { id: 5, name: 'Родительская категория 5'},
                ],
                categoryList:   new Map(),
            }
        },
        computed: {},
        watch: {
            'showPopupCategory'(value) {
                this.showModal = value;
            }
        },
        methods: {
            closePopup() {
                this.showModal = false;
                this.$emit('close_popup', this.showModal);
            },
            createCategory() {
                if (this.editCategory) return;
                
                if(this.defaultCategory.name) {
                    // const arr = new Map();
                    let parent = false;
                    let id = Date.now();
                    let children = [];

                    let newCategory = {
                        id,
                        name: this.defaultCategory.name,
                        parent,
                        ...this.defaultCategory,
                        children
                    }
                    if (this.defaultCategory.parentCategory) {
                        parent = true;
                        console.log('1', this.categoryList);
                        let currentCategory = this.categoryList[this.defaultCategory.parentCategory ];
                        currentCategory.children.push(newCategory)
                        localStorage.setItem('categoryList', JSON.stringify(this.categoryList));
                        this.showModal = false;
                        this.$emit('close_popup', this.showModal);
                        return 
                    }
                    console.log('cr', this.categoryList);
                    this.categoryList.set(id, newCategory)
                    // this.categoryList && newCategory.name && this.categoryList.push(arr)
                    this.categoryList && newCategory.name && localStorage.setItem('categoryList', JSON.stringify([...this.categoryList]));
                    this.showModal = false;
                    this.$emit('close_popup', this.showModal);
                }
            }
        }
    };
</script>

<style lang="scss">
    .category {
        position: fixed;
        z-index: 1;
        padding-top: 55px;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        background: rgba(10, 14, 32, 0.4);

        &-modal {
            font-family: "Montserrat";
            padding: 32px 32px 24px;
            background: #ffffff;
            border-radius: 10px;
            max-width: 826px;
            margin: auto;
        }
        &-form {
            margin: auto;
            background: white;
            display: flex;
            flex-direction: column;
            gap: 16px;
            flex-grow: 1;
       
        }

        &__title {
            font-weight: 600;
            font-size: 20px;
            line-height: 28px;
            color: #303446;
            margin-top: 0;
            margin-bottom: 16px;
        }

        &__name {
            cursor: pointer;
            font-family: "Montserrat";
            background: #ffffff;
            border: 1px solid #d9dde6;
            border-radius: 4px;
            padding: 11px 12px 13px 16px;
            font-weight: 500;
            font-size: 14px;
            line-height: 20px;
            color: #a0a6bf;
            width: 100%;

            &::placeholder {
                color: #a0a6bf;
            }

            &:focus {
                outline: 1px solid #d9dde6;
            }
        }

        &-footer {
            border-top: 1px solid #bfc3d5;
            padding-top: 16px;
            display: flex;
            gap: 24px;
            margin-top: 360px;

            & button {
                padding: 10px 16px;
                width: 100%;
                justify-content: center;
            }
        }
    }
</style>
