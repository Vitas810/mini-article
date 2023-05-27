<template>
    <div>
        <btn text="Создать категорию"></btn>
    </div>
</template>

<script>
    document.title = 'article-page';
    import btn from '@/components/btn.vue';
    
    export default {
        name: 'Article-header',
        components: {
            btn
        }
        }
</script>
