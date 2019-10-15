<template>
  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" aria-hidden="true" class="c-icon"><polyline points="20 6 9 17 4 12"></polyline></svg>
</template>

<script>
  export default {
    name: 'IconCheck'
  }
</script>

<style lang="scss">

svg:not(:root) {
  overflow: hidden;
}
.c-icon {
  vertical-align: sub;
  fill: none;
  stroke: currentColor;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.c-marked-text__icon svg {
  display: block;
}
.c-icon:not(.c-icon--size-auto) {
    width: 1.13em;
    height: 1.13em;
    stroke-width: 2px;
}
</style>
