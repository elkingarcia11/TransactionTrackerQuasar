<template>
  <q-page class="row items-center justify-evenly">
    <TransactionsTable ref="transactionsTable" />
  </q-page>
</template>

<script lang="ts">
import TransactionsTable from 'components/TransactionsTable.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TransactionsPage',
  components: { TransactionsTable },
});
</script>
