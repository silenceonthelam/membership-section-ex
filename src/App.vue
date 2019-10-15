<template>
  <div class="container" id="app">
    <FormSection
      sectionTitle="Membership"
    />
  </div>
</template>

<script>
import FormSection from './components/FormSection'

export default {
  name: 'app',
  components: {
    FormSection,
  }
}
</script>

<style lang="scss">
.container {
  margin-bottom: 50px;
  margin-top: 35px;
  position: relative;
}
</style>
