<template lang="pug">
.row
  .container
    post(:post="post")

</template>

<script>
import Post from '~/components/post/Post.vue'
import { getContent } from '~/utils/golos'


export default {
  //layout: 'full-width',
  scrollToTop: true,

  components: {
    Post
  },

  async asyncData ({ store, route, error, app }) {
    let { author, permlink } = route.params
    let post = await getContent(author.toLowerCase(), permlink)

    if (!post) return error({ statusCode: 404, message: 'Post not found' })

    return { post }
  }
}

</script>
