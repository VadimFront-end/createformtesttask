<template>
  <div id="app">
    <Form/>
  </div>
</template>

<script>
import Form from './components/Form'

export default {
  name: 'App',
  components: {
    Form
  }
}
</script>

<style lang="sass">
#app
  margin: auto
  display: flex
  align-items: center
  justify-content: center
  height: 100%
  min-height: 100vh
</style>
