<template>
  <div>
    <h1 style="text-align: center;margin-bottom: 10px">Адрес</h1>
    <InputForm
        :id="'indexHome'"
        :label="'Индекс'"
        @getInput="data => this.indexHome=data"/>
    <InputForm
        :id="'Country'"
        :label="'Страна'"
        @getInput="data => this.Country=data"/>
    <InputForm
        :id="'region'"
        :label="'Область'"
        @getInput="data => this.region=data"/>
    <InputForm
        :id="'city'"
        :label="'Город'"
        @getInput="data => this.city=data"/>
    <div v-show="$v.city.$invalid&&error" class="error">Обязательное поле</div>
    <InputForm
        :id="'street'"
        :label="'Улица'"
        @getInput="data => this.street=data"/>
    <InputForm
        :id="'home'"
        :label="'Дом'"
        @getInput="data => this.home=data"/>
  </div>
</template>

<script>
import InputForm from './InputForm'
import { required} from 'vuelidate/lib/validators'

export default {
  name: "SecondPartForm",
  components: {
    InputForm
  },
  props: {
    check: {
      type: Boolean,
      default() {
        return false
      }
    }
  },
  data: () => ({
    indexHome: '',
    Country: '',
    region: '',
    city: '',
    street: '',
    home: '',
    error: false
  }),
  validations: {
    city: {
      required
    }
  },
  updated() {
    console.log(!this.$v.$invalid)
    this.$emit('ready', !this.$v.$invalid);
  },
  watch: {
    check() {
      this.$emit('ready', !this.$v.$invalid);
      this.error = true;
    }
  }
}
</script>
