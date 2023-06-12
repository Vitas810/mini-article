<template>
    <main class="main">
        <section class="main-default" v-if="posts.length !== 0">
            <h3>Пока нет статей</h3>
            <span class="main-default__description">Создайте свою первую  категорию и добавьте в неё статьи.</span>
            <btn text="Создать категорию" />
        </section>
        <template v-else>
            <art-category />
        </template>
    </main>
</template>

<script>
    import btn from '@/components/btn.vue';
    import ArtCategory from '@/views/ArtCategory.vue';

    export default {
        name: 'ArtMain',
        components: {
            btn,
            ArtCategory,
        },
        data() {
            return {
                posts: [],
            }
        }
    }
</script>

<style lang="scss">
    .main {
        &-default {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 144px;
            & h3 {
                font-weight: 600;
                font-size: 16px;
                line-height: 24px;
                text-align: center;
                color: #303446;
                margin-bottom: 4px;
            }
            &__description {
                display: inline-block;
                font-weight: 500;
                font-size: 14px;
                line-height: 22px;
                text-align: center;
                color: #6A6E7E;
                max-width: 260px;
                margin-bottom: 16px;
            }
        }
    }
</style>