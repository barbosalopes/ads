<template>
  <div class="stack">
    <Stack />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Stack from '@/components/Stack.vue';

export default Vue.extend({
  name: 'stack',
  components: {
    Stack,
  },
});
</script>
