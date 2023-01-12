<template>
  <q-page class="row items-center justify-evenly">
    <TransactionsTable />
    <FabComponent />
  </q-page>
</template>

<script lang="ts">
import TransactionsTable from 'components/TransactionsTable.vue';
import FabComponent from 'components/FabComponent.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TransactionsPage',
  components: { TransactionsTable, FabComponent },
});
</script>
