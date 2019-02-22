<template>
  <div id="app">
    <NavMenu />
  </div>
</template>

<script>
import Login from '@/components/Login/login'
import NavMenu from '@/components/NavMenu'

export default {
  name: 'App',
  components: {
    Login,
    NavMenu
  }
}
</script>

<style lang="scss" scoped="scoped">
#app {
  height: 100%;
}
</style>
