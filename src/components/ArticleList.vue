<template>
    <div class="feed">
        <div class="feed-title is-size-3">
            {{feed.title}}
        </div>
        <div v-if="loading">
            <div class="loader">Loading...</div>
        </div>
        <div class="articles-container">
            <ArticleListItem v-for="(article, index) in feed.items"
                             :key="index"
                             :article="article"/>
        </div>
    </div>
</template>

<script>
    import ArticleListItem from './ArticleListItem.vue';
    import RSSParser from 'rss-parser';

    export default {
        name: 'ArticleList',
        components: {
            ArticleListItem
        },
        props: {
            feedUrl: String
        },
        created() {
            this.fetchData();
        },
        watch: {
            feedUrl() {
                this.fetchData();
            }
        },
        data() {
            return {
                feed: []
            };
        },
        methods: {
            async fetchData() {
                this.loading = true;
                this.feed = [];
                if (!this.feedUrl) {
                    console.log('Empty feed url given, please try again');
                    this.loading = false;
                    return;
                }
                try {
                    const urlWithCorsAnywhere = `${this.feedUrl}`;
                    const data = await fetch(urlWithCorsAnywhere);
                    if (data.ok) {
                        const text = await data.text();
                        const rssParser = new RSSParser();
                        rssParser.parseString(text, (err, parsed) => {
                            this.loading = false;
                            if (err) {
                                console.log(`Error occurred while parsing feed: ${err.toString()}`);
                            } else {
                                this.feed = parsed;
                            }
                        });
                    } else {
                        console.log("Error occurred while fetching feed");
                        this.loading = false;
                    }
                } catch (error) {
                    console.log(error.toString());
                    this.loading = false;
                }
            }
        }
    }
</script>

<style scoped>
    .feed {
        padding: 20px 50px;
        width: 800px;
        height: 100vh;
        overflow-y: auto;
    }

    .feed-title {
        margin-bottom: 20px;
    }

    .articles-container {
    }

    .loader {
        font-size: 50px;
    }
</style>
