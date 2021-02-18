<template lang="pug">
  form.friends-possible(@submit.prevent="onSearchUsers" action="#")
    h4.friends-possible__title Параметры поиска
    .friends-search
      .friends-search__row
        .friends-search__block
          label.search__label(for="friends-search-name") Имя:
          input.search__input(type="text" id="friends-search-name" v-model="first_name")
        .friends-search__block
          label.search__label(for="friends-search-lastname") Фамилия:
          input.search__input(type="text" id="friends-search-lastname" v-model="last_name")
      .friends-search__block
        label.search__label Возраст:
        .search__row
          select.select.friends-search__select(v-model.number="age_from")
            option(value="null" disabled) От
            option(v-for="option in ages" :value="option") От {{option}}
          span.search__age-defis —
          select.select.friends-search__select(v-model.number="age_to")
            option(value="null" disabled) До
            option(v-for="option in ages" :value="option") До {{option}}
      .friends-search__block
        .friends-search__row
          label.search__label(for="friends-search-country") Страна:
          input.search__input(type="text" id="friends-search-country" v-model="country")
        .friends-search__row
          label.search__label(for="friends-search-city") Город:
          input.search__input(type="text" id="friends-search-city" v-model="city")
    button.friends-possible__btn(type="submit")
      simple-svg(:filepath="'/static/img/search.svg'")
      span.friends-possible__link Искать друзей
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'FriendsSearch',
  data: () => ({
    first_name: null,
    last_name: null,
    age_from: null,
    age_to: null,
    country_id: null,
    city_id: null,
    offset: 0,
    itemPerPage: 20
  }),
  methods: {
    ...mapActions('global/search', ['searchUsers', 'clearSearch']),
    onSearchUsers() {
      let { first_name, last_name, age_from, age_to, country, city } = this
      this.searchUsers({ first_name, last_name, age_from, age_to, country, city })
    }
  },
  beforeDestroy() {
    this.clearSearch()
  },
  computed: {
    ages() {
      let result = []
      for (let i = 0; i <= 100; i++) {
        result.push(i);
      }
      return result
    }
  }
}
</script>

<style lang="stylus">
@import '../../assets/stylus/base/vars.styl';

.friends-search {
  margin-top: 25px;
  padding-top: 20px;
  margin-bottom: 30px;
  border-top: 1px solid #E6E6E6;
}

.friends-search__row {
  @media (max-width: breakpoint-xl) {
    display: flex;

    .friends-search__block {
      flex: auto;
    }

    .friends-search__block + .friends-search__block {
      margin-top: 0;
      margin-left: 12px;
    }
  }
}

.friends-search__row + .friends-search__block {
  margin-top: 15px;
}

.friends-search__block {
  &+& {
    margin-top: 15px;
  }
}

.friends-search__select {
  display: block;
  width: 100%;

  &+& {
    margin-left: 12px;
  }
}
</style>
