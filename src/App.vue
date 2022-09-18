<template>
  <div id="app" class="app">
    <div class="app__container">
      <form>
        <InputValidation v-for="(input, index) in inputs" :key="index" :item="input" @input="inputValue"/>
        <SelectOption v-for="(select, index) in selects" :key="index" :item="select" @selected="selectedValue"/>
      </form>
      <button id="submit" disabled @click="submit">Submit</button>
      <p>* required fields</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import InputValidation from './components/InputValidation.vue'
import SelectOption from './components/SelectOption.vue'

export default Vue.extend({
  name: 'App',
  components: {
    InputValidation,
    SelectOption
  },
  methods: {
    selectedValue (value, key) {
      this.selects[key].value = value
      this.empty = this.selects[key].value === ''
    },
    inputValue (value, key) {
      this.inputs[key].value = value
    },
    submit () {
      alert('Gratulacje! Formularz został poprawnie wysłany!')
    }
  },
  data () {
    return {
      inputs: {
        name: {
          label: 'Imię',
          required: true,
          regex: /^[A-Za-z]{3,16}$/i,
          active: true,
          value: String
        }
      },
      selects: {
        brands: {
          label: 'Marka Auta',
          required: true,
          active: true,
          options: ['Audi', 'Honda', 'Opel', 'Mitsubishi', 'Mazda', 'Toyota', 'Ferrari', 'Lamborgini', 'Jeep', 'Range Rover'],
          value: String
        }
      }
    }
  }
})
</script>

<style lang="scss">
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  flex-direction: column;
}
.app__container {
  width: 320px;
  padding: 40px 0px 40px 0px;
  box-shadow: 1px 1px 10px lightgrey;
  border-radius: 25px;
}

.label  {
  display: inline;
  justify-self: center;
  padding: 10px;
  &-required::after {
    color: red;
    content: '*';
    display: inline;
    padding: 10px;
  }
}
</style>
