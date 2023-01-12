<template>
  <q-page class="row items-center justify-evenly">
    <LogInComponent />
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import LogInComponent from 'src/components/LogInComponent.vue';

export default defineComponent({
  name: 'IndexPage',
  components: { LogInComponent },
});
</script>
