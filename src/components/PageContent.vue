<template>
  <main class="tb-content">
    <page-title/>
    <slot/>
  </main>
</template>
<script>
import PageTitle from '@/components/PageTitle'
export default {
  components: {
    PageTitle
  }
}
</script>

<style lang="scss" scoped>

</style>
