<template>
    <section class="popup js-popup-remove" v-if="showPopup">
        <div class="popup-modal">
            <question />
            <h2>Удалить категорию?</h2>
            <h3>Все дочерние категории удалятся.</h3>

            <div class="popup-modal__btns">
                <btn text="Удалить" :show-icon="false"/>
                <btn-cancel />
            </div>
        </div>
    </section>
</template>

<script>
    import question from '@/assets/svg/question-circle.svg';
    import btnCancel from "@/components/btn-cancel.vue";
    import btn from '@/components/btn.vue';

    export default {
        name: 'ArtPopupRemove',
        props: {
            showPopupRemoveCategory: {
                type: Boolean,
            }
        },
        components: {
            question,
            btnCancel,
            btn
        },
        created() {
            document.addEventListener('click', e => {
                let popup = document.querySelector('.js-popup-remove');
                let target = e.target;
   
                if (popup == target) {
                    this.showPopup = false;
                    this.$emit('close-popup', this.showModal);
                }
            });
        },
        data() {
            return {
                showPopup: false
            }
        },
        watch: {
            'showPopupRemoveCategory'(val) {
                this.showPopup = val;
            }
        }
    }
</script>

<style lang="scss" scoped>
    .popup {
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
            padding: 32px 64px 46px;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #ffffff;
            border-radius: 10px;
            max-width: 467px;
            margin: auto;
            & h2 {
                font-weight: 600;
                font-size: 16px;
                line-height: 24px;
                text-align: center;
                color: #303446;
                margin-top: 16px;
                margin-bottom: 4px;
            }
            & h3 {
                font-weight: 500;
                font-size: 14px;
                line-height: 22px;
                text-align: center;
                color: #6A6E7E;
                margin-bottom: 32px;
            }
            &__btns {
                display: flex;
                gap: 8px;
            }
        }
    }
</style>