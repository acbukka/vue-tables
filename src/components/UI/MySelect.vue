<template>
  <div class="select__wrapper">
    <h3 class="select__title">
      <slot></slot>
    </h3>
    <select class="select" @change="changeOption">
      <option
        class="select__option"
        v-for="(option, index) in options"
        :value="option"
        :selected="index === 0"
      >
        {{ option }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'my-select',
  props: {
    modelValue: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit('update:modelValue', event.target.value);
    },
  },
}
</script>

<style lang="scss" scoped>
.select {
  width: 100%;
  padding: 0 3px;
  font-family: 'Nunito', sans-serif;
  font-size: 1.2em;
  cursor: pointer;
  height: 38px;
  border: 1px solid #d1d5db;
  background: transparent;
  box-shadow: 0 1px 2px rgb(0 0 0 / 5%);
  border-radius: 6px;
  color: #374151;
  &__wrapper {
    width: 100%;
    align-items: center;
    display: flex;
  }
  &__title {
    white-space: nowrap;
    margin-right: 5px;
  }
}
</style>