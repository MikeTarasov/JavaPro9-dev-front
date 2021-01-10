<template lang="pug">
  .search-all
    search-block(title="Люди", id="users" all)
      .friends__list
        friends-block(v-for="user in users" :key="user.id" :info="user")
    search-block(title="Новости", id="news" all)
      news-block(v-for="n in news" :key="n.id" :info="n")
</template>

<script>
import { mapGetters } from 'vuex'
import SearchBlock from '../Search/Block'
import FriendsBlock from '../Friends/Block'
import NewsBlock from '../News/Block'
export default {
  name: 'SearchAll',
  components: { SearchBlock, FriendsBlock, NewsBlock },
  computed: {
    ...mapGetters('global/search', ['getResultById']),
    news() {
      return this.getResultById('news')
    },
    users() {
      return this.getResultById('users')
    }
  }
}
</script>
