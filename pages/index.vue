<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        Hello, World!
      </h1>
      <br/>
      <h2>Love, Nuxt.</h2>
      <br/>
      <div class="links">
        <!-- nuxt-link will loop through the posts. :to needs the name of the route, and id of the params -->
        <nuxt-link
          v-for="post in posts"
          :to="{name: 'posts-id', params: {id: post.id}}"
          :key="post.id"
          class="button--grey"
        >
          {{post.title}}
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // seo tags go here, under head. It looks the same as the data method - a function that returns an object with the content 
  head () {
    return {
      title: 'Home page 🔥',
      meta: [
        { name: 'twitter:title', content: 'Nuxt Fundamentals by Vue School' },
        { name: 'twitter:description', content: 'Nuxt + Vue School = 🍕' },
        { name: 'twitter:image', content: '/logo.vue' },
        { name: 'twitter:card', content: 'summary_lage_card' }
      ]
    }
  },
  computed: {
    posts () {
      return this.$store.state.posts.all
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
  'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  letter-spacing: 1px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
}
.links {
  padding-top: 15px;
}
</style>