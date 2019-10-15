<template>
  <li
    class="list-item"
    :class="{
      active: isSelected,
    }"
    @click="$emit('click-item', item)"
  >
    {{ item.text }}
  </li>
</template>

<script>
export default {
  name: 'DropdownListItem',
  props: {
    isSelected: { type: Boolean, default: false },
    item: { type: Object, required: true },
  },
}
</script>

<style lang="scss">
  .list-item {
    border-bottom: 1px solid #ededed;
    color: #0d0d0d;
    height: 52px;
    line-height: 52px;
    margin: 0;
    padding: 0 12px;

    &:hover,
    &.active {
      background-color: #ededed;
      color: #1178ce;
    }
  }
</style>
