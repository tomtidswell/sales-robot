<template>
  <b-navbar :mobile-burger="true">
    <template slot="brand">
      <b-navbar-item tag="NuxtLink" :to="{ path: '/' }">
        <header class="logo-set" @click.meta.right="enableAdmin">
          <div class="sale">
            Sale
          </div>
          <div class="robot">
            Robot
          </div>
        </header>
      </b-navbar-item>
    </template>
    <template slot="start">
      <b-navbar-item tag="NuxtLink" :to="{ path: '/' }">
        <b-icon icon="magnify" size="is-small" />
      </b-navbar-item>
      <b-navbar-dropdown label="Categories" arrowless hoverable boxed>
        <b-navbar-item
          v-for="(data, name) in categories"
          :key="name"
          tag="NuxtLink"
          :to="{ path: `/category?${data.websafeName}` }"
        >
          {{ data.displayName }}
        </b-navbar-item>
      </b-navbar-dropdown>
      <b-navbar-dropdown label="Shops" arrowless hoverable boxed>
        <b-navbar-item
          v-for="(data, name) in retailers"
          :key="name"
          tag="NuxtLink"
          :to="{ path: `/retailer?${data.websafeName}` }"
        >
          {{ data.displayName }}
        </b-navbar-item>
      </b-navbar-dropdown>
    </template>

    <template slot="end">
      <b-navbar-dropdown label="Admin" arrowless hoverable boxed right>
        <b-navbar-item tag="NuxtLink" :to="{ path: '/scrape-history' }">
          Scrape history
        </b-navbar-item>
        <b-navbar-item v-if="admin" tag="NuxtLink" :to="{ path: './scrape-settings' }">
          Scrape settings
        </b-navbar-item>
        <b-navbar-item v-if="admin" tag="NuxtLink" :to="{ path: './category-map' }">
          Category map config
        </b-navbar-item>
      </b-navbar-dropdown>
      <b-navbar-item tag="div">
        <div class="buttons">
          <a class="button is-primary">Sign up</a>
          <a class="button is-light"> Log in </a>
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script>
import { retailerConfig, categoryConfig } from '../assets/config'

export default {
  name: 'Navigation',
  data () {
    return {
      admin: false,
      shop: null,
      category: null,
      filterOptions: []
    }
  },
  computed: {
    retailers: () => {
      return retailerConfig
    },
    categories: () => {
      return categoryConfig
    }
  },
  created () {
  },
  methods: {
    enableAdmin () {
      // console.log('Enabling admin')
      this.admin = !this.admin
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

.navbar-link{
  &:hover{
    text-decoration: underline;
  }
}

header.logo-set{
  display: flex;
  align-items: center;
  font-size: 3em;
  .sale{
    font-family: 'Fredericka the Great', cursive;
    color: #f81363;
    padding-top: 4px;
  }
  .robot{
    font-family: 'Bungee Shade', cursive;
    padding-bottom: 4px;
    letter-spacing: -2px;
  }
}

</style>
