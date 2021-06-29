<template>
  <div id="app">
    <BaseHeader />
    <router-view class="container"/>
    <BaseFooter />
  </div>
</template>

<script>
import BaseHeader from '@/components/BaseHeader'
import BaseFooter from '@/components/BaseFooter'

export default {
  name: 'App',
  components: {
    BaseHeader,
    BaseFooter
  }
}
</script>

<style lang="scss" scoped>
#app {
  box-sizing: border-box;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #37474f;
  margin: 60 auto;
  padding: 0;
}
.container {
  padding-bottom: 4rem;
}
</style>
