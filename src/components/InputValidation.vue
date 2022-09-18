<template>
  <div class="input_validation">
    <label id="label" class="label" :for="item.label" :class="{ 'label-required': item.required }"> {{ item.label }} </label>
    <input class="input empty" :name="item.label" placeholder="Placeholder..." :disabled="!item.active" @blur="validateInput($event);">
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'InputValidation',
  props: {
    item: Object
  },
  methods: {
    validateInput (event) {
      if (!this.item.regex.test(event.target.value)) {
        event.target.classList.add('input-error')
        event.target.classList.remove('empty')
        document.getElementById('submit')?.setAttribute('disabled', '')
        this.onChange(event, true)
      } else {
        event.target.classList.remove('input-error')
        this.onChange(event, false)
        event.target.classList.remove('empty')
        if (document.querySelectorAll('.empty').length <= 0) {
          document.getElementById('submit')?.removeAttribute('disabled')
        }
      }
    },
    onChange (event) {
      this.$emit('input', event.target.value, this.$vnode.key)
    }
  }
})
</script>

<style scoped lang="scss">
.input_validation {
  padding: 10px;
  align-items: center;
  display: flex;
  flex-direction: column;
  .input {
    display: block;
    border: 1px rgb(185, 185, 185) solid;
    border-radius: 4px;
    background: white;
    padding: 10px;
    &:focus {
      box-shadow: 1px 1px 10px grey;
      border: 0px gray solid;
      &-visible {
        outline: none;
      }
    }
    &-error {
      border: 1px red solid;
      &::before {
        content:'Popraw wartość';
      }
    }
  }
}
</style>
