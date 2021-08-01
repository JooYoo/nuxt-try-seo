<template>
  <article>
    <p>{{ article.title }}</p>
    <p>{{ article.description }}</p>
    <p>Article last updated: {{ article.updatedAt }}</p>

    <nuxt-content :document="article" />
  </article>
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('articles', params.slug).fetch()

      return { article }
    },
    head() {
      return {
        title: this.article.title,
        meta: [{
          hid: 'description',
          name: 'description',
          content: this.article.description
        }]
      }
    }
  }

</script>

<style>

</style>