<template>
  <div class="container">
    <article>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
    <aside>
      <h3>Posts you might enjoy</h3>
      <ul>
        <li v-for="related in relatedPosts">
          <!-- use nuxt-link instead of a tag so that browser doesn't have to reload the page. Pass a path to nuxt link -->
          <nuxt-link :to="`/posts/${related.id}`">
            {{related.title}}
          </nuxt-link>
        </li>
      </ul>
    </aside>
  </div>
</template>

<script>
  export default {
    head () {
    return {
      title: this.post.title,
      meta: [
        { name: 'twitter:title', content: this.post.title },
        { name: 'twitter:description', content: this.post.content },
        { name: 'twitter:image', content: '/logo.vue' },
        { name: 'twitter:card', content: 'summary_lage_card' }
      ]
    }
  },
    data () {
      return {
        //to access the id specified in the url, and pick the corresponding post from the array and show to users
        id: this.$route.params.id,
        // posts array moved to posts.js in store
        /* posts: [
          {
            id: 'balut',
            title: 'What is Balut?',
            content: 'If someone placed balut on your plate, you might think they were serving you a hardboiled egg. That is, until you cracked it open and a fully intact duck embryo spilled out. Balut, considered a delicacy in many Asian countries, is produced when fertilized duck eggs are placed in warm sunlight. After about eight days, the eggs are held up to the light and checked to ensure that the budding embryo is ready. Then, the eggs are cooked and served with a dash of salt and a few squirts of lemon juice.'
          },
          {
            id: 'whereIsIt',
            title: 'Where is the sign in button?',
            content: 'I\'ve stalked the forum for a while, want to sign up but cannot find the button.'
          },
          {
            id: 'how',
            title: 'How do I fix this?',
            content: 'Please help fix'
          }
        ] */
      }
    },
    //
    computed: {
      //computed property post that will give us the active post
      post () {
        // this code using the posts coming from the store. Nuxt auto injects the store into all components. So $store, then go to the state, then go to the posts.js module inside store, then grab all the posts that live in the all property
        return this.$store.state.posts.all.find(post => post.id === this.id)
        // without using vuex store 👇
        // return this.posts.find(post => post.id === this.id)
      },
      //this will return all the posts except for the active one
      relatedPosts () {
        return this.$store.state.posts.all.filter(post => post.id !== this.id)
        // without using vuex store 👇
        // return this.posts.filter(post => post.id !== this.id)
      }
    }
  }
</script>

<style scoped>
  .container {
    display: flex;
    justify-content: space-between;
    line-height: 1.5;
  }
  article * {
    margin-bottom: 1rem;
  }
  aside {
    min-width: 280px;
    max-width: 280px;
    padding-left: 2rem;
  }
  .title {
    font-size: 2rem;
  }
</style>