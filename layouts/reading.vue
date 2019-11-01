<template>
  <div>
    <main-header></main-header>
    <nuxt />
    <main-footer></main-footer>
  </div>
</template>
<script>
import MainHeader from './MainHeader'
import MainFooter from './MainFooter'

export default {
  components: {
    MainHeader,
    MainFooter
  }
}
</script>
