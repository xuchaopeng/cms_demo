<template>
  <div id="app"><Container /></div>
</template>

<script>
import Layout from '@/components/Layout'
import Container from '@/components/Container'
import Login from '@/components/Login/login'
import NavMenu from '@/components/NavMenu'

export default {
  name: 'App',
  components: {
    Login,
    NavMenu,
    Layout,
    Container
  }
}
</script>

<style lang="scss" scoped="scoped">
#app {
  height: 100%;
  min-width: 600px;
  max-width: 1920px;
  margin: 0 auto;
}
</style>
