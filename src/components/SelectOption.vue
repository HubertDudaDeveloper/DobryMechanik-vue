<template>
    <div class="selectoption">
      <label id="label" class="label" :for="item.label" :class="{ 'label-required': item.required }"> {{ item.label }} </label>
        <select name="item.label" class="select empty" placeholder="Marka Auta" :disabled="!item.active" @input="onChange($event)">
            <option value="" disabled selected>Wybierz opcje</option>
            <option v-for="(i, k) in item.options" :key="k" class="select__option" :value="i"> {{ i }} </option>
        </select>
    </div>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'SelectOption',
  props: {
    item: Object
  },
  methods: {
    onChange: function (event) {
      this.$emit('selected', event.target.value, this.$vnode.key)
      event.target.classList.remove('empty')
      if (document.querySelectorAll('.input-error').length <= 0 && document.querySelectorAll('.empty').length <= 0) {
        document.getElementById('submit')?.removeAttribute('disabled')
      }
    }
  }
})
</script>
<style lang="scss">
.selectoption {
  padding: 10px;
  align-items: center;
  display: flex;
  flex-direction: column;
  .select {
    padding: 10px;
    width: 60%;
    border: 1px solid lightgray;
    border-radius: 6px;
    &:focus {
      box-shadow: 1px 1px 10px grey;
      border: 0px gray solid;
      &-visible {
        outline: none;
      }
    }
  }
}
</style>
