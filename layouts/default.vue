<template>
  <div>
    <Navigation />
    <section class="main-content columns">
      <!-- <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">General</p>
        <ul class="menu-list">
          <li v-for="(item, key) of items" :key="key">
            <nuxt-link :to="item.to" exact-active-class="is-active">
              <b-icon :icon="item.icon" /> {{ item.title }}
            </nuxt-link>
          </li>
        </ul>
      </aside> -->

      <div class="container column is-10">
        <nuxt />
      </div>
    </section>

  </div>
</template>

<script>
export default {
  data () {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  }
}
</script>

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
