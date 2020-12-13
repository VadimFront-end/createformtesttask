<template>
  <div>
    <h1 style="text-align: center;margin-bottom: 10px">Общие данные</h1>
    <InputForm
        :id="'name'"
        :label="'Имя'"
        @getInput="data => this.name=data"/>
    <div v-show="$v.name.$invalid&&error" class="error">Обязательное поле</div>
    <InputForm
        :id="'surname'"
        :label="'Фамилию'"
        @getInput="data => this.surname=data"/>
    <div v-show="$v.surname.$invalid&&error" class="error">Обязательное поле</div>
    <InputForm
        :id="'middle-name'"
        :label="'Отчество'"
        @getInput="data => this.middleName=data"/>
    <InputForm
        :id="'birthday'"
        :label="'Дата рождения'"
        :type="'date'"
        @getInput="data => this.birthday=data"/>
    <div v-show="$v.birthday.$invalid&&error" class="error">Обязательное поле</div>
    <InputForm
        :id="'number'"
        :placeholder="'7XXXXXXXXXX'"
        :type="'tel'"
        :label="'Номер телефона'"
        @getInput="data => this.number=data"/>
    <div v-if="!$v.number.required&&error" class="error">Обязательное поле</div>
    <div v-else-if="(!$v.number.checkNumber||!$v.number.maxLength)&&error" class="error">Неверный формат</div>
    <label for="man" style="margin-right: 5px">Муж</label>
    <input
        id="man"
        type="radio"
        :checked="userSex ? 'checked': ''"
        @click="userSex=!userSex">
    <label for="woman" style="margin-right: 5px">Жен</label>
    <input
        id="woman"
        type="radio"
        :checked="!userSex ? 'checked': ''"
        @click="userSex=!userSex">
    <div class="for-input">Группа</div>
    <SelectComponent
        style="margin: 5px 0"
        :multiSelect="true"
        :list="clientsGroup"
        @getItem="data => this.clientsGroupSelected = data"/>
    <div v-show="$v.clientsGroupSelected.$invalid&&error" class="error">Обязательное поле</div>
    <div class="for-input" style="margin: 5px 0">Лечащий врач</div>
    <SelectComponent
        :list="doctors"
        @getItem="data => this.doctorSelected = data"/>
    <div style="margin: 5px 0">
      <input type="checkbox" v-model="isSendSMS">
      <span style="margin-left: 5px">Не отправлять СМС</span>
    </div>
  </div>
</template>

<script>
import InputForm from './InputForm'
import SelectComponent from './SelectComponent'
import {minLength, maxLength, required} from 'vuelidate/lib/validators'

export default {
  name: "FirstPartForm",
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
    name: '',
    surname: '',
    middleName: '',
    birthday: '',
    number: '',
    userSex: true,
    clientsGroup: ['VIP', 'Проблемные', 'ОМС'],
    doctors: ['Иванов', 'Захаров', 'Чернышева'],
    doctorSelected: '',
    clientsGroupSelected: '',
    isSendSMS: false,
    error: false
  }),
  validations: {
    name: {
      required
    },
    surname: {
      required
    },
    birthday: {
      required
    },
    number: {
      required,
      maxLength: maxLength(11),
      checkNumber(number) {
        return /7[0-9]{10}/.test(number);
      }
    },
    clientsGroupSelected: {
      required,
      minLength: minLength(2)
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
