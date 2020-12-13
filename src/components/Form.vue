<template>
  <form id="form">
    <h2 v-show="isCreated" style="color: green;text-align: center">Пользователь создан!</h2>
    <FirstPartForm
        v-show="showThisPart === 1"
        :check="check"
        @ready="data => {this.firstError = data;createUser()}"/>
    <SecondPartForm
        v-show="showThisPart === 2"
        :check="check"
        @ready="data => {this.secondError = data;createUser()}"/>
    <ThirdPartForm
        v-show="showThisPart === 3"
        :check="check"
        @ready="data => {this.thirdError = data;createUser()}"/>
    <div class="footer-form">
      <div
          class="select-part-form"
          :style="{border: firstError ? '2px dotted #E35757': showThisPart===1 ? '2px dotted #6B6B9E': ''}"
          @click="showThisPart=1">1
      </div>
      <div
          class="select-part-form"
          :style="{border: showThisPart===2 ? '2px dotted #6B6B9E': ''}"
          @click="showThisPart=2">2
      </div>
      <div
          class="select-part-form"
          :style="{border: showThisPart===3 ? '2px dotted #6B6B9E': ''}"
          @click="showThisPart=3">3
      </div>
    </div>
    <button
        class="create-button"
        @click.prevent="check=!check"
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
    check: false,
    isCreated: false,
    firstError: false,
    secondError: false,
    thirdError: false
  }),
  methods: {
    createUser() {
      if(!this.isCreated)
        if(this.firstError&&this.secondError&&this.thirdError) this.isCreated = true;
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
  border: 1px solid #6B6B9E

.create-button
  display: block
  margin: 15px auto 0
  padding: 5px
  cursor: pointer
</style>
