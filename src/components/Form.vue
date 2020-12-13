<template>
  <form id="form">
    <h2 v-show="isCreated" style="color: green;text-align: center">Пользователь создан!</h2>
    <FirstPartForm
        v-show="showThisPart === 1"
        :check="isChecked"
        @ready="data => this.firstError = data"/>
    <SecondPartForm
        v-show="showThisPart === 2"
        :check="isChecked"
        @ready="data => this.secondError = data"/>
    <ThirdPartForm
        v-show="showThisPart === 3"
        :check="isChecked"
        @ready="data => this.thirdError = data"/>
    <div class="footer-form">
      <div
          class="select-part-form"
          :style="{borderColor: !firstError&&isChecked ? '#E35757': '#6B6B9E',
                   borderStyle: showThisPart===1 ? 'dotted': ''}"
          @click="showThisPart=1">1
      </div>
      <div
          class="select-part-form"
          :style="{borderColor: !secondError&&isChecked ? '#E35757': '#6B6B9E',
                   borderStyle: showThisPart===2 ? 'dotted': ''}"
          @click="showThisPart=2">2
      </div>
      <div
          class="select-part-form"
          :style="{borderColor: !thirdError&&isChecked ? '#E35757': '#6B6B9E',
                   borderStyle: showThisPart===3 ? 'dotted': ''}"
          @click="showThisPart=3">3
      </div>
    </div>
    <button
        class="create-button"
        @click.prevent="createUser"
        v-show="showThisPart===3">Создать
    </button>
  </form>
</template>

<script>
import FirstPartForm from './FirstPartForm'
import SecondPartForm from './SecondPartForm'
import ThirdPartForm from './ThirdPartForm'

export default {
  name: "Form",
  components: {
    FirstPartForm,
    SecondPartForm,
    ThirdPartForm
  },
  data: () => ({
    showThisPart: 1,
    isReady: true,
    isChecked: false,
    isCreated: false,
    firstError: false,
    secondError: false,
    thirdError: false
  }),
  methods: {
    createUser() {
      this.isChecked = true;
      if (this.firstError && this.secondError && this.thirdError) this.isCreated = true;
    }
  }
}
</script>

<style lang="sass">
.input-place
  margin: 5px 0
  width: 100%
  padding: 5px
  color: #6B6B9E
  background: #1C1C42
  border-radius: 3px

.for-input
  color: #AAAACD

#form
  padding: 15px 10px 12px
  width: 310px
  background: #0A0C1E
  box-shadow: 0 0 12px 4px #27279B
  border-radius: 5px

.footer-form
  display: flex
  align-items: center
  justify-content: space-evenly

.select-part-form
  padding: 1px 5px
  cursor: pointer
  border-color: #6B6B9E
  border-style: solid
  border-width: 2px

.create-button
  display: block
  margin: 15px auto 0
  padding: 5px
  cursor: pointer
</style>
