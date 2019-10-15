<template>
  <label class="picker__option" for="optId">
    <input
      type="radio"
      :id="optId"
      :value="optId"
      :checked="checked"
      @change="handleUpdateSelected"
    />
    <slot></slot>
  </label>
</template>

<script>
  export default {
    name: 'PickerOption',
    props: {
      checked: { type: Boolean, default: false },
      handleUpdateSelected: { type: Function, required: true },
      optId: { type: String, required: true },
    },
  }
</script>

<style lang="scss">
  .picker__option {
    flex: 0 1 100%;
    list-style: none;
    margin: 0;
    padding: 0 15px;
    position: relative;

    &:first-of-type {
      padding-left: 0;
    }
    &:last-of-type {
      padding-right: 0;
    }

    :hover {
      cursor: pointer;
    }

    & input[type=radio] {
      -webkit-appearance: none;
      display: inline-block;
      height: 100%;
      left: 0;
      margin: 0;
      padding: 0;
      position: absolute;
      top: 0;
      width: 100%;

      &:active,
      &:focus {
        outline: none;
      }
    }
  }
</style>
