<template>
  <div class="input__wrapper">
    <h3 class="input__title">
      <slot></slot>
    </h3>
    <input :value="modelValue" @input="updateInput" class="input" type="text">
  </div>
</template>

<script>
export default {
  name: 'my-input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped>
.input {
  width: 100%;
  padding: 0 3px;
  font-family: 'Nunito', sans-serif;
  font-size: 1.2em;
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
    margin-left: 15px;
    white-space: nowrap;
    margin-right: 5px;
  }
}

@media (max-width: 767px) {
  .input__title {
    margin-left: 0;
  }
}
</style>