<template>
  <div class="checkout-page-wrapper">
    <progress-bar />
    <div class="container">
      <first-step />
    </div>
  </div>
</template>

<script>
import progressBar from './components/progressBar.vue'
import firstStep from './components/firstStep.vue'
export default {
  name: 'App',
  components: {
    progressBar,
    firstStep,
  }
}
</script>

<style lang="stylus">
body
  background-color #FFFAE6 !important
#app
  font-family 'Montserrat', sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
