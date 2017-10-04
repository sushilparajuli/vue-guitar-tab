<template>
  <div class="white elevation-2">
    <v-toolbar flat dense class="primary" dark>
      <v-toolbar-title class="white--text"><h6 class="mb-0"> {{title}} </h6></v-toolbar-title>
      <v-spacer></v-spacer>
      <slot name="action" />
    </v-toolbar>
    <div class="pl-4 pr-4 pb-2 pt-2">
      <slot>
        No slot content defined
      </slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'panel',
    props: [
      'title'
    ]
  }
</script>

