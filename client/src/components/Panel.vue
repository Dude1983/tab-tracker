<template>
  <v-card class="elevation-12">
    <v-toolbar dark color="teal">
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <slot name="action" />
    </v-toolbar>

    <v-card-text>
        <slot>
          No slot content defined.
        </slot>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: [
    'title'
  ]
}
</script>

<style scoped>

</style>
