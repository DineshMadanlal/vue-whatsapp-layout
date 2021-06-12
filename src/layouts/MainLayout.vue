<template>
  <!-- Whatsapp layout -->
  <q-layout view="lhh lpR lff">
    <!-- Left side drawer -->
    <q-drawer
      v-model="leftDrawerOpen"
      overlay
      bordered
      side="left"
      behavior="desktop"
    >
      <!-- drawer content -->
    </q-drawer>

    <!-- Right side content -->
    <q-page-container>
    </q-page-container>

  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false // state variable to open/close the sidebar
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
