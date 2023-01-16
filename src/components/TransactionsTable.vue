<template>
  <div class="table-container">
    <q-table
      v-touch-hold.mouse="handleHold"
      title="Transactions"
      title-class="titleClass"
      :rows="rows"
      :columns="columns"
      :selection="selection"
      :filter="filter"
      v-model:selected="selected"
      @row-click="selectRow"
      row-key="name"
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

  <FabAddComponent v-if="selection == 'none'" />
  <q-page-sticky
    position="bottom-right"
    :offset="[18, 18]"
    v-else-if="selected.length < 2"
  >
    <FabEditComponent :item="selected" />
    <q-btn
      round
      class="q-ml-lg"
      color="red"
      icon="delete"
      size="lg"
      @click="deleteRows"
    />
  </q-page-sticky>
  <q-page-sticky position="bottom-right" :offset="[18, 18]" v-else>
    <q-btn
      round
      class="q-ml-lg"
      color="red"
      icon="delete"
      size="lg"
      @click="deleteRows"
    />
  </q-page-sticky>
</template>

<script>
import FabAddComponent from 'src/components/FabAddComponent.vue';
import FabEditComponent from 'src/components/FabEditComponent.vue';
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
      selected: ref([]),
      columns,
      rows,
      selection: ref('none'),
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
    handleHold() {
      if (this.selection == 'none') {
        this.selection = 'multiple';
      } else {
        this.selection = 'none';
      }
    },
    selectRow(evt, row, index) {
      console.log(evt, index);
      if (this.selection == 'multiple') {
        const i = this.selected.indexOf(row);
        if (i == -1) {
          this.selected.push(row);
        } else {
          this.selected.splice(i, 1);
        }
      }
    },
    deleteRows() {
      console.log('Deleting: ', JSON.stringify(this.selected));
    },
  },
  components: { FabAddComponent, FabEditComponent },
};
</script>
