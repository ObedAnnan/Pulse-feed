<template>

    <div class="article box">
        <a :href="article.link"
           class="article-title">
            {{article.title}}
        </a>
        <div class="article-body">
            <p class="article-content"
               v-html="article.content">
            </p>
        </div>
    </div>

</template>

<script>

    export default {
        name: 'ArticleListItem',
        props: {
            article: Object,
        },
        methods: {}
    }


</script>

<style scoped>
    .article {
        color: #424242;
        display: flex;
        padding: 20px 24px;
        flex-direction: column;
        justify-content: space-between;
        word-break: break-word;
    }

    .article-title {
        color: #424242;
        font-size: 18px;
        font-weight: 600;
        margin-bottom: 8px;
        text-decoration: none;
    }

    .article-title:hover {
        color: #7A7A7A;
        cursor: pointer;
        text-decoration: none;
    }

    .article-content {
        font-size: 14px;
        margin-top: 8px;
    }
</style>
