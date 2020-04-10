<template>
  <q-page class="flex flex-center">
    <q-card class="my-card">
      <q-card-section class="">
        <div class="col">
          <div class="row">
            <q-input v-model="username" label="User Name" />
          </div>
          <div class="row">
            <q-input v-model="postingkey" label="Posting Key" />
          </div>
        </div>

        <q-item v-for="(item, index) in discussions" :key="index"  clickable v-ripple>
          <q-item-section>
            <q-item-label>{{ item.title }}</q-item-label>
            <q-item-label caption>{{ item.author }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-card-section>
      <q-card-actions align="right">
        <q-btn push >Login</q-btn>
        <q-btn push >Post</q-btn>
      </q-card-actions>
    </q-card>
  </q-page>
</template>

<script>
const hivejs = require('@hivechain/hivejs')

export default {
  name: 'PageIndex',
  data () {
    return {
      discussions: [],
      username: null,
      postingkey: null
    }
  },
  created () {
    const self = this
    hivejs.api.getAccounts(['helo'], (err, users) => {
      console.log('users', users, err)
    })

    hivejs.api.getDiscussionsByBlog({
      tag: 'helo',
      limit: 10
    }, (err, results) => {
      console.log('posts', results, err)
      self.discussions = results
    })

    console.log('this.discussions', this.discussions)
  },
  methods: {

  }
}
</script>
