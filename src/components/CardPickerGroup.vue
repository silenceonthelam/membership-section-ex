<template>
  <fieldset>
    <legend class="group__label">
      Select your membership type below:
    </legend>
    <div class="picker">
      <picker-option
        v-for="pickerOption in pickerOptions"
        :key="pickerOption.id"
        :handleUpdateSelected="handleUpdateSelected"
        :checked="selectedCardId === pickerOption.id"
        :optId="pickerOption.id"
      >
        <card
          :cardTitle="pickerOption.cardTitle"
          :cardIcon="pickerOption.cardIcon"
          :cardDescription="pickerOption.cardDescription"
          :cardPrice="pickerOption.cardPrice"
          :cardRequirements="pickerOption.cardRequirements"
          :isSelected="selectedCardId === pickerOption.id"
          :hasSelection="!!selectedCardId"
          :hasError="shouldShowError"
        />
      </picker-option>
    </div>
    <p class="error-text">
      <span v-if="shouldShowError">
        {{ errorMsg }}
      </span>
    </p>
    <p class="body-text--sm note">
      <slot name="note"></slot>
    </p>
  </fieldset>
</template>

<script>
import Card from './Card'
import PickerOption from './PickerOption'

export default {
  name: 'CardPickerGroup',
  components: {
    Card,
    PickerOption,
  },
  props: {
    errorMsg: { type: String, default: '' },
    handleUpdateSelected: { type: Function, required: true },
    pickerOptions: { type: Array, required: true },
    selectedCardId: { type: String, default: null },
    shouldShowError: { type: Boolean, default: false },
  },
}
</script>

<style lang="scss">
  .picker {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding-left: 0;

    &:hover {
      .card {
        opacity: .7;
      }
    }
  }
  .note {
    padding-top: 25px;
  }
  .group__label {
    margin-bottom: 1em;
    padding-bottom: 1.5rem;
  }
</style>
