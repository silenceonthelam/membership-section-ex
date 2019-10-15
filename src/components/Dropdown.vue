<template>
  <section class="dropdown">
    <h3 class="dropdown__header">
      {{ dropdownHeader }}
    </h3>
    <p class="dropdown__description">
      {{ dropdownDescription }}
    </p>

    <div
      class="dropdown__container"
      :class="{
        open: isDropdownOpen
      }"
      @click="toggleDropdown"
    >
      <p
        class="dropdown__label"
        :class="{
          active: selectedItem,
        }"
      >
        {{ dropdownPlaceholder }}
      </p>
      <p class="dropdown__selected">
        <span v-if="selectedItem">
          {{ selectedItem.text }}
        </span>
      </p>
      <ul class="dropdown__list" v-if="isDropdownOpen">
        <dropdown-list-item
          v-for="item in dropdownItems"
          :key="item.text"
          :item="item"
          :isSelected="selectedItem && item.text === selectedItem.text"
          v-on:click-item="handleUpdateSelected"
        />
      </ul>
    </div>
    <p class="error-text">
      <span v-if="shouldShowError">
        {{ errorMsg }}
      </span>
    </p>
  </section>
</template>

<script>
  import DropdownListItem from './DropdownListItem'

  export default {
    name: 'Dropdown',
    components: {
      DropdownListItem
    },
    props: {
      dropdownDescription: { type: String, required: true },
      dropdownHeader: { type: String, required: true },
      dropdownItems: { type: Array, required: true },
      dropdownPlaceholder: { type: String, required: true },
      errorMsg: { type: String, default: '' },
      handleUpdateSelected: { type: Function, required: true },
      selectedItem: { type: Object, default: null },
      shouldShowError: { type: Boolean, default: false },
    },
    data() {
      return {
        isDropdownOpen: false,
      }
    },
    methods: {
      toggleDropdown() {
        this.isDropdownOpen = !this.isDropdownOpen
      },
    }
  }
</script>

<style scoped lang="scss">
  .dropdown {
    margin: 0;
    position: relative;
    width: 100%;
  }
  .dropdown__header {
    font: normal 1.25em/1.3 "Circular Bold";
    margin-bottom: .2em;
  }
  .dropdown__description {
    margin-bottom: 1em;
    padding: 0;
  }

  .dropdown__container {
    border-radius: 2px;
    box-shadow: inset 0 0 0 1px #85868c;
    font-size: 18px;
    height: 40px;
    line-height: 40px;
    margin: .5rem 0;
    position: relative;
    width: 66.67%;

    &::after {
      content: url(data:image/svg+xml;base64,PHN2ZyBjbGFzcz0nZmVhdGhlciBmZWF0aGVyLWNoZXZyb24tZG93biBzYy1pd3NLYkkgY25sY29RJyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHdpZHRoPScyNCcgaGVpZ2h0PScyNCcgdmlld0JveD0nMCAwIDI0IDI0JyBmaWxsPSdub25lJyBzdHJva2U9J2N1cnJlbnRDb2xvcicgc3Ryb2tlLXdpZHRoPScyJyBzdHJva2UtbGluZWNhcD0ncm91bmQnIHN0cm9rZS1saW5lam9pbj0ncm91bmQnIGFyaWEtaGlkZGVuPSd0cnVlJyBkYXRhLXJlYWN0aWQ9JzI2Nic+PHBvbHlsaW5lIHBvaW50cz0nNiA5IDEyIDE1IDE4IDknPjwvcG9seWxpbmU+PC9zdmc+);
      position: absolute;
      right: 10px;
      top: 6px;
      transition: transform .3s ease;
    }

    &:hover {
      cursor: pointer;
    }

    &.open {
      box-shadow: inset 0 0 0 1px #1178ce;

      &::after {
        transform: rotate(180deg) translateY(12px);
      }
    }
  }
  .dropdown__label {
    color: #6d6d6d;
    display: inline-block;
    margin: 0;
    margin-bottom: .5rem;
    overflow: hidden;
    padding: 0 10px;
    pointer-events: none;
    position: absolute;
    text-overflow: ellipsis;
    transition: all .3s ease;
    white-space: nowrap;
    z-index: 3;

    &.active {
      background-color: white;
      font-size: 12px;
      color: #6d6d6d;
      line-height: 12px;
      padding-left: 0;
      padding-right: 2px;
      padding-bottom: 2px;
      transform: translate(12px, -7px);
    }
  }
  .dropdown__selected {
    color: #0d0d0d;
    height: 40px;
    line-height: 40px;
    margin: 0;
    padding: 0 12px;
  }
  .dropdown__list {
    background-color: #fff;
    border: 1px solid #1178ce;
    border-radius: 2px;
    border-top-left-radius: 0;
    border-top-right-radius: 0;
    border-top: none;
    margin: 0;
    max-height: 300px;
    overflow-y: scroll;
    padding: 0;
    position: relative;
    top: -2px;
    z-index: 1;
  }
</style>
