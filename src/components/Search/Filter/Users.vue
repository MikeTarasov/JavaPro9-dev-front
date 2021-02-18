<template lang="pug">
  .search-filter
    .search-filter__block.name
      label.search__label(for="search-people-name") Имя:
      input.search__input(type="text" id="search-people-name" v-model="first_name")
    .search-filter__block.lastname
      label.search__label(for="search-people-lastname") Фамилия:
      input.search__input(type="text" id="search-people-lastname" v-model="last_name")
    .search-filter__block.age
      label.search__label Возраст:
      .search__row
        select.select.search-filter__select(v-model.number="age_from")
          option(value="null" disabled) От
          option(v-for="option in ages" :value="option") От {{option}}
        span.search__age-defis —
        select.select.search-filter__select(v-model.number="age_to")
          option(value="null" disabled) До
          option(v-for="option in ages" :value="option") До {{option}}
    .search-filter__block.country
      label.search__label(for="search-people-country") Страна:
      input.search__input(type="text" id="search-people-country" v-model="country")
    .search-filter__block.city
      label.search__label(for="search-people-city") Город:
      input.search__input(type="text" id="search-people-city" v-model="city")
    .search-filter__block.btn-news(@click.prevent="onSearchUsers")
      button-hover Применить
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'SearchFilterUsers',
  data: () => ({
    first_name: null,
    last_name: null,
    age_from: null,
    age_to: null,
    country: null,
    city: null,
    offset: 0,
    itemPerPage: 20
  }),
  methods: {
    ...mapActions('global/search', ['searchUsers']),
    onSearchUsers() {
      let { first_name, last_name, age_from, age_to, country, city } = this
      this.searchUsers({ first_name, last_name, age_from, age_to, country, city })
    }
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
