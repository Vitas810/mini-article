<template>
    <div ref="select" class="__select" data-state="">
        <div class="__select__title" :class="{'open-dropdown': showFieldSearch}" data-default="Option 0">
            <span ref="title">{{ title }}</span>
            <input type="text"
                class="__select__search"
                v-model="search"
                ref="search"
                v-show="showFieldSearch">
        </div>
        <div class="__select__content"  ref="selectContent">
            <template v-for="(option, idx) in searchOptions">
                <template v-if="option.id">
                    <input :id="`singleSelect_${idx}`"
                        class="__select__input"
                        type="radio"
                        v-model="selected"
                        :value="option.id"
                        @input="$emit('input', $event.target.value)"
                        name="singleSelect" />
                    <label :for="`singleSelect_${idx}`" class="__select__label">{{ option.name }}</label>
                </template>
            </template>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ArtSelect',
        props: {
            title: {
                type: String,
                require: true,
                default: 'Название'
            },
            options: {
                type: [Array, Object]
            }
        },
        data() {
            return {
                search: null,
                showFieldSearch: false,
                selected: null
            }
        },
        computed: {
            searchOptions() {
                if (!this.search) {
                    return this.options;
                }

                return this.options.filter((option) => {
                    return option.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
                });
            }
        },
        mounted() {
            this.init();
        },
        methods: {
            init() {
                const selectSingle = this.$refs.select;
                const selectSingle_title = selectSingle && selectSingle.querySelector('.__select__title');
                const selectSingle_labels = selectSingle && selectSingle.querySelectorAll('.__select__label');

                selectSingle_title && selectSingle_title.addEventListener('click', (event) => {
                    if ('active' === selectSingle.getAttribute('data-state')) {
                        selectSingle.setAttribute('data-state', '');
                        this.showFieldSearch = false;
                        this.search = null;
                    } else {
                        selectSingle.setAttribute('data-state', 'active');
                        this.showFieldSearch = true;
                    }

                    if (event.target == this.$refs.search) {
                        selectSingle.setAttribute('data-state', 'active');
                        this.showFieldSearch = true;
                    }
                });

                for (let i = 0; i < selectSingle_labels.length; i++) {
                    selectSingle_labels[i] && selectSingle_labels[i].addEventListener('click', (evt) => {
                        this.$refs.title.innerText = evt.target.textContent;
                        selectSingle.setAttribute('data-state', '');
                        this.showFieldSearch = false;
                        console.log('e', evt.target);
                        // this.search = null;
                    });
                }

                // const reset = document.querySelector('.reset');
                // reset && reset.addEventListener('click', () => {
                //     selectSingle_title.textContent = selectSingle_title.getAttribute('data-default');
                //     this.showFieldSearch = false;
                // });
            },
        }
    }
</script>

<style lang="scss" scoped>
    .open-dropdown {
        font-size: 11px !important;
        line-height: 13px !important;
        flex-direction: column;
        align-items: flex-start !important;
        padding: 5px 7px 6px 12px !important;
        & input {
            border: none;
            padding: 4px 0;
            outline: transparent;
            padding-right: 30px;
            width: 90%;
        }
    }
    .__select {
        position: relative;
        width: 100%;
        height: 46px;
        margin: 0 auto;

        &[data-state="active"] {
            .__select__title {
                &::before {
                    transform: translate(-3px, -50%) rotate(-45deg);
                }

                &::after {
                    transform: translate(3px, -50%) rotate(45deg);
                }
            }
            .__select__content {
                opacity: 1;
            }
            
            .__select__input + .__select__label {
                max-height: 40px;
                font-size: 14px;
                line-height: 22px;
                color: #4D5163;
            }
        }
    }
    .__select__title {
        font-family: 'Montserrat';
        font-weight: 500;
        font-size: 14px;
        line-height: 22px;
        display: flex;
        align-items: center;
        color: #A0A6BF;
        display: flex;
        align-items: center;
        width: 100%;
        height: 100%;
        padding: 10px 7px 12px 12px;
        border: 1px solid #D9DDE6;
        border-radius: 4px;
        cursor: pointer;
        &:focus {
            color: #303446;
        }

        &::before,
        &::after {
            content: "";
            position: absolute;
            top: 50%;
            right: 16px;
            display: block;
            width: 10px;
            height: 2px;
            transition: all 0.3s ease-out;
            background-color: #A0A6BF;
            transform: translate(-3px, -50%) rotate(45deg);
        }
        &::after {
            transform: translate(3px, -50%) rotate(-45deg);
        }
        &:hover {
            border-color: #BFC3D5;
            &::before,
            &::after {
                background-color: #BFC3D5;
            }
        }
    }
    .reset {
        display: flex;
        width: 230px;
        padding: 8px 16px;
        margin: 0 auto;
        margin-bottom: 10px;
        border: solid 1px #c7ccd1;
        border-radius: 5px;
        transition: all 0.2s ease-out;
        cursor: pointer;
        font-weight: bold;
        background-color: #ffffff;
        color: #333333;
    
        &:hover {
            background-color: #D8093A;
            color: #ffffff;
        }
    }
    .__select__content {
        position: absolute;
        top: 48px;
        left: 3px;
        display: flex;
        flex-direction: column;
        width: calc(100% - 6px);
        background-color: #ffffff;
        border-top: none;
        border-bottom-left-radius: 5px;
        border-bottom-right-radius: 5px;
        box-shadow: 0px 10px 40px rgba(0, 0, 0, 0.07);
        transition: all 0.3s ease-out;
        opacity: 0;
        z-index: 8;
    }
    .__select__input {
        display: none;

        &:checked + label {
            background-color: #dedede;
        }
        &:disabled + label {
            opacity: 0.6;
            pointer-events: none;
        }
    }
    .__select__label {
        display: flex;
        align-items: center;
        width: 100%;
        height: 40px;
        max-height: 0;
        padding: 0 16px;
        transition: all 0.2s ease-out;
        cursor: pointer;
        overflow: hidden;
        & + input + & {
            border-top: 0 solid #C7CCD160;
        }

        &:hover {
            background: rgba(48, 52, 70, 0.03);
            border-radius: 5px;
            color: #4D5163;
        }
    }
</style>