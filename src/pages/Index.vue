<template>
  <q-page class="flex flex-center">
    <q-card>
      <q-card-section>
        <q-item v-for="(post, index) in discussions" :key="index"  clickable v-ripple>
          <q-item-section>
            <q-item-label>{{ post.title }}</q-item-label>
            <q-item-label caption>{{ post.author }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
const hivejs = require('@hivechain/hivejs')

export default {
  name: 'PageIndex',
  data () {
    return {
      discussions: []
    }
  },
  created () {
    const self = this

    hivejs.api.getDiscussionsByBlog({ tag: 'helo', limit: 10 }, (err, res) => {
      self.discussions = res
      console.log(err)
    })
  }
}
</script>
