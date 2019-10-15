<template>
  <form class="form" v-on:submit.prevent="onSubmit">
    <header class="form__header">
      <h2 class="form__header__title">{{ sectionTitle }}</h2>
    </header>

    <div class="form-section-content">
      <card-picker-group
        :errorMsg="nonePickedError"
        :selectedCardId="cardPicked"
        :shouldShowError="shouldShowNonePickedError"
        :handleUpdateSelected="updateSelectedCard"
        :pickerOptions="pickerOptions"
      >
        <template v-slot:note>
          *If you are under 18 years of age please <a href="//www.ascap.com/helpcenter#underAge" target="_blank">read more about how to join ASCAP.</a>
        </template>
      </card-picker-group>

      <dropdown
        v-if="shouldShowSelect"
        :dropdownHeader="dropdownHeader"
        :dropdownDescription="dropdownDescription"
        :dropdownItems="dropdownItems"
        :dropdownPlaceholder="dropdownPlaceholder"
        :errorMsg="notSelectedError"
        :shouldShowError="shouldShowNotSelectedError"
        :selectedItem="selectedItem"
        :handleUpdateSelected="updateSelectedItem"
      />

      <p class="body-text--sm">
        ASCAP uses TINCheck and SmartyStreets to verify certain information provided by you in connection with your application. Any information
        processed by TINCheck and SmartyStreets shall be subject to the privacy policies of
        <a href="https://www.tincheck.com/pages/tincheck-agreement" target="_blank">TINCheck</a> and
        <a href="https://smartystreets.com/legal/privacy-policy" target="_blank">SmartyStreets</a>.
      </p>
    </div>

    <div class="buttons">
      <a href="//www.ascap.com">
        <button class="btn cancel" type="button">
          Cancel
        </button>
      </a>
      <button class="btn" type="submit">
        Continue
      </button>
    </div>
  </form>
</template>

<script>
import CardPickerGroup from './CardPickerGroup'
import Dropdown from './Dropdown'

export default {
  name: 'SimpleForm',
  components: {
    CardPickerGroup,
    Dropdown,
  },
  props: {
    sectionTitle: { type: String, required: true },
  },
  data() {
    // the following specific form data would ideally
    // come from a store in a real-world app
    return {
      cardPicked: null,
      dropdownHeader: 'Publisher Company Type',
      dropdownDescription: 'Please select the federal tax classification of your publisher company',
      dropdownPlaceholder: 'Publisher Company Type',
      dropdownItems: [
        { id: 0, text: 'Individual / Sole proprietor or Single-member LLC' },
        { id: 1, text: 'C Corporation' },
        { id: 2, text: 'S Corporation' },
        { id: 3, text: 'LLC - C Corporation' },
        { id: 4, text: 'LLC - S Corporation' },
        { id: 5, text: 'LLC - Partnership' },
        { id: 6, text: 'Partnership' },
        { id: 7, text: 'Trust / Estate' },
        { id: 8, text: 'OTHER' },
      ],
      hasAttemptedSubmit: false,
      nonePickedError: 'Please select your membership type.',
      notSelectedError: 'Please select your publisher company type.',
      pickerOptions: [
        {
          id: 'memberTypeBoth',
          cardTitle: 'Writer & Publisher',
          cardIcon: 'quavers-and-briefcase',
          cardDescription: 'ASCAP royalties are split evenly between Writers and Publishers. Join as both to ensure you get paid everything you deserve.',
          cardPrice: '100',
          cardRequirements: [
            'Legal Name',
            'Mailing Address',
            'Valid Email Address',
            'SSN/ITIN or EIN',
            'Must be 18 or older*'
          ]
        },
        {
          id: 'memberTypeWriter',
          cardTitle: 'Writer',
          cardIcon: 'quavers',
          cardDescription: 'A Writer is someone who creates a musical composition: the melody, harmony, lyrics, arrangements, beats, etc.',
          cardPrice: '50',
          cardRequirements: [
            'Legal Name',
            'Mailing Address',
            'Valid Email Address',
            'SSN/ITIN',
            'Must be 18 or older*'
          ]
        },
        {
          id: 'memberTypePublisher',
          cardTitle: 'Publisher',
          cardIcon: 'briefcase',
          cardDescription: 'A Publisher is a person or company that handles the business side of music. Publishers may control the copyrights of a musical composition, licensing, etc.',
          cardPrice: '50',
          cardRequirements: [
            'Legal Name',
            'Mailing Address',
            'Valid Email Address',
            'SSN/ITIN or EIN',
            'Must be 18 or older*'
          ]
        }
      ],
      selectedItem: null,
    }
  },
  computed: {
    hasErrors() {
      return this.shouldShowNonePickedError || this.shouldShowNotSelectedError
    },
    shouldShowNonePickedError() {
      return this.hasAttemptedSubmit && !this.cardPicked
    },
    shouldShowNotSelectedError() {
      return this.hasAttemptedSubmit && !this.selectedItem
    },
    shouldShowSelect() {
      return this.cardPicked === 'memberTypePublisher' ||
        this.cardPicked === 'memberTypeBoth'
    },
  },
  methods: {
    onSubmit(e) {
      this.hasAttemptedSubmit = true
      if (this.hasErrors) return

      console.log('submitting...')
      // then would call whatever needed to happen with
      // form data containing this.cardPicked and this.selectedItem
    },
    updateSelectedItem(item) {
      this.selectedItem = item
    },
    updateSelectedCard(e) {
      this.cardPicked = e.target.value
      this.hasAttemptedSubmit = false;
    },
  }
}
</script>

<style lang="scss">
  .form {}
  .form__header {}
  .form__header__title {
    font: normal 1.5em/1.29 "Circular Black";
    margin-bottom: .33em;
  }
  .buttons {
    padding: .5em 0 3rem;
  }
  .btn {
    display: inline-block;
    font-weight: 400;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 2px;
    border: 0;
    margin: 0;
    display: inline-block;
    font-family: 'Circular Bold',sans-serif;
    overflow: hidden;
    color: #fff;
    padding: 8px 20px;
    background-color: #1178ce;
    line-height: 18px;
    height: 40px;
    transition: all .3s ease-in-out;
    margin-right: 10px;
    text-transform: uppercase;
    margin-bottom: .5rem;

    &:hover,
    &:active,
    &:focus {
      background-color: #175da7;
      outline: none;
    }
  }
  .btn.cancel {
    background-color: #fff;
    color: #0d0d0d;
    border: 1px solid #ededed;

    &:hover,
    &:focus {
      background-color: #fafafa;
      border: 1px solid #cecece;
    }
  }
  .btn:not(:disabled):not(.disabled) {
    cursor: pointer;
  }
</style>
