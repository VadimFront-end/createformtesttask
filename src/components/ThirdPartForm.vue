<template>
  <div>
    <h1 style="text-align: center;margin-bottom: 10px">Паспорт</h1>
    <SelectComponent
        :list="docTypes"
        @getItem="data => this.docTypesSelected = data"/>
    <div v-show="$v.docTypesSelected.$invalid&&error" class="error">Обязательное поле</div>
    <InputForm
        :id="'series'"
        :label="'Серия'"
        @getInput="data => this.series=data"/>
    <InputForm
        :id="'number'"
        :label="'Номер'"
        @getInput="data => this.number=data"/>
    <InputForm
        :id="'issued'"
        :label="'Кем выдан'"
        @getInput="data => this.issued=data"/>
    <InputForm
        :id="'issuedDate'"
        :label="'Дата выдачи'"
        :type="'date'"
        @getInput="data => this.issuedDate=data"/>
    <div v-show="$v.issuedDate.$invalid&&error" class="error">Обязательное поле</div>
  </div>
</template>

<script>
import InputForm from './InputForm'
import SelectComponent from './SelectComponent'
import {required} from "vuelidate/lib/validators";
export default {
  name: "ThirdPartForm",
  components: {
    InputForm,
    SelectComponent
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
    docTypes: ['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение'],
    docTypesSelected: '',
    series: '',
    number: '',
    issued: '',
    issuedDate: '',
    error: false
  }),
  validations: {
    docTypesSelected: {
      required
    },
    issuedDate: {
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
