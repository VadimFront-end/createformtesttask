<template>
  <div class="input-form">
    <label :for="id" class="for-input">{{ label }}</label>
    <input
        :type="type"
        :max="type === 'date' ? '2015-01-01': ''"
        class="input-place"
        :placeholder="placeholder"
        :id="id"
        v-model.trim="userData"
        @change="$emit('getInput', userData)">
  </div>
</template>

<script>

export default {
  name: "InputForm",
  props: {
    label: {
      type: String,
      default() {
        return ''
      }
    },
    id: {
      type: String,
      default() {
        return '';
      }
    },
    type: {
      type: String,
      default() {
        return 'text'
      }
    },
    placeholder: {
      type: String,
      default() {
        return ''
      }
    }
  },
  data: () => ({
    userData: ''
  })
}
</script>

<style lang="sass">

</style>
