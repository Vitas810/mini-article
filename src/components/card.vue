<template>
    <div class="card">
        <div class="card-top">
            <div class="card-top__like">
                <like-default />
                <span>40</span>
            </div>
            <pen class="card-top__edite" />
        </div>

        <div class="card-img">
            <img  src="../assets/card-img.jpg" alt="card">
        </div>

        <div class="card-bottom">
            <h3 class="card-bottom__title">Заголовок</h3>
            <span class="card-bottom__description">Идейные соображения высшего порядка, а также сложившаяся структура организации играет важную роль в
                формировании существенных финансовых и административных условий. Равным образом начало повседневной
                работы по формированию позиции представляет собой интересный эксперимент проверки направлений
                прогрессивного развития.</span>
        </div>
    </div>
</template>

<script>
    import likeDefault from '@/assets/svg/like-default.svg';
    import pen from '@/assets/svg/pen.svg'
    export default {
        name: 'ArtCard',
        components: {
            likeDefault,
            pen
        }
    }
</script>

<style lang="scss">
    .card {
        padding: 16px;
        border: 1px solid #BFC3D5;
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        gap: 8px;
        max-width: 291px;
        &-top {
            display: flex;
            align-items: center;
            justify-content: space-between;
            &__like {
                display: flex;
                align-items: center;
                cursor: pointer;
                & span {
                    font-weight: 500;
                    font-size: 12px;
                    line-height: 15px;
                    text-align: center;
                    color: #A0A6BF;
                }
            }
            &__edite {
                cursor: pointer;
            }
        }
        &-img {
            max-width: 100%;
            height: 80px;
            & img {
                width: 100%;
                height: 100%;
                object-fit: cover;
            }
        }
        &-bottom {
            &__title {
                font-weight: 600;
                font-size: 16px;
                line-height: 24px;
                color: #303446;
                margin-bottom: 8px;
                margin-top: 0;
            }
            &__description {
                font-weight: 500;
                font-size: 14px;
                line-height: 22px;
                color: #6A6E7E;
                display: -webkit-box;
                -webkit-line-clamp: 5;
                -webkit-box-orient: vertical;
                overflow: hidden;
                text-overflow: ellipsis; 
            }
        }
    }
</style>
