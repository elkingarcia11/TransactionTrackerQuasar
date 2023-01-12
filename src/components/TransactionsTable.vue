<template>
  <div class="table-container">
    <q-table
      title="Transactions"
      title-class="titleClass"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :filter="filter"
      separator="cell"
    >
      <template v-slot:top-right>
        <q-input
          borderless
          dense
          debounce="300"
          v-model="filter"
          placeholder="Search"
        >
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
    </q-table>
  </div>
</template>

<script>
import { ref } from 'vue';
import { api } from 'boot/axios';

const columns = [
  {
    name: 'name',
    required: true,
    label: 'FULL NAME',
    align: 'left',
    field: 'name',
    format: (val) => `${val}`,
    sortable: false,
  },
  {
    name: 'invoice',
    required: true,
    label: 'INVOICE NO.',
    align: 'left',
    field: 'invoice',
    format: (val) => `${val}`,
    sortable: false,
  },
  {
    name: 'paid',
    required: true,
    label: 'AMOUNT PAID ($)',
    align: 'left',
    field: 'paid',
    format: (val) => `${val}`,
    sortable: false,
  },
  {
    name: 'receipt',
    required: true,
    label: 'RECEIPT NO.',
    align: 'left',
    field: 'receipt',
    format: (val) => `${val}`,
    sortable: false,
  },
  {
    name: 'date',
    required: true,
    label: 'DATE POSTED',
    align: 'left',
    field: 'date',
    format: (val) => `${val}`,
    sortable: false,
  },
];

const rows = [
  {
    name: 'Frozen Yogurt',
    invoice: '12456',
    paid: 159,
    receipt: 6.0,
    date: 24,
  },
  {
    name: 'Elkin Yogurt',
    invoice: '12456',
    paid: 159,
    receipt: 6.0,
    date: 24,
  },
  {
    name: 'Frozen Garcia',
    invoice: '12456',
    paid: 159,
    receipt: 6.0,
    date: 24,
  },
];

export default {
  setup() {
    return {
      filter: ref(''),
      columns,
      rows,
    };
  },
  methods: {
    getTransactions() {
      api
        .get('/api/tracker/transactions')
        .then((response) => {
          rows = response.data;
        })
        .catch(() => {
          console.log('Failed to fetch transactions');
        });
    },
  },
};
</script>
