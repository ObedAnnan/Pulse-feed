<template>
    <div class="columns">
        <div class="column is-one-quarter no-padding">
            <SubscriptionList @change-active-subscription="setActiveSubscription"></SubscriptionList>
        </div>
        <div class="column no-padding">
            <ArticleList :feedUrl="feedUrl"/>
        </div>
    </div>
</template>

<script>
    import SubscriptionList from './components/SubscriptionList'
    import ArticleList from "./components/ArticleList";

    export default {
        name: 'App',
        components: {
            ArticleList,
            SubscriptionList
        },
        data() {
            return {
                feedUrl: ''
            };
        },
        methods: {
            setActiveSubscription(url) {
                this.feedUrl = url;
            },
        },
    }
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
