<template>
  <div>
    <h1>Blog Posts</h1>
    <ul>
      <li v-for="article of articles" :key="article.slug">
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
          <div>
            <h2>{{ article.title }}</h2>
            <p>by {{ article.author.name }}</p>
            <p>{{ article.description }}</p>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const articles = await $content('articles')
        .only(['title', 'description', 'slug', 'author'])
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        articles
      }
    },
    head() {
      return {
        title: "zhuyu is learning nuxt in DE",
        meta: [{
          hid: 'description',
          name: 'description',
          content: "zhuyu is learning nuxt in DE"
        }]
      }
    }
  }
</script>
