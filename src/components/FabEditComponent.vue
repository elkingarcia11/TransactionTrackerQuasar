<template>
  <q-dialog v-model="prompt">
    <q-card class="q-pa-lg" style="min-width: 350px">
      <div class="text-h5 text-center">Edit transaction</div>
      <q-input
        autofocus
        ref="nameInput"
        class="q-pt-md"
        outlined
        color="secondary"
        v-model="name"
        label="Full Name"
        @keyup.enter="nextInput(1)"
      />
      <q-input
        ref="invoiceInput"
        class="q-pt-md"
        outlined
        color="secondary"
        v-model="invoice"
        label="Invoice No."
        @keyup.enter="nextInput(2)"
      />
      <q-input
        ref="amountInput"
        class="q-pt-md"
        outlined
        color="secondary"
        v-model="paid"
        label="Amount Paid"
        @keyup.enter="nextInput(3)"
      />
      <q-input
        ref="receiptInput"
        class="q-pt-md"
        outlined
        color="secondary"
        v-model="receipt"
        label="Receipt No."
        @keyup.enter="nextInput(4)"
      />

      <q-input
        class="q-pt-md"
        outlined
        color="secondary"
        v-model="date"
        label="Date Posted"
      >
        <template v-slot:append>
          <q-icon name="event" class="cursor-pointer">
            <q-popup-proxy
              ref="dateProxy"
              cover
              transition-show="scale"
              transition-hide="scale"
            >
              <q-date v-model="date" color="secondary" mask="YYYY-MM-DD">
                <div class="row items-center justify-end">
                  <q-btn v-close-popup label="Done" color="secondary" flat />
                </div>
              </q-date>
            </q-popup-proxy>
          </q-icon>
        </template>
      </q-input>

      <q-card-actions align="center" class="text-primary">
        <q-btn
          flat
          color="secondary"
          label="Cancel"
          v-close-popup
          @click="cancelTransaction"
        />
        <q-btn
          flat
          color="secondary"
          label="Submit"
          v-close-popup
          @click="submitTransaction"
        />
      </q-card-actions>
    </q-card>
  </q-dialog>
  <q-btn round color="green" icon="edit" size="lg" @click="triggerDialogue" />
</template>

<script>
import { ref } from 'vue';

const d = new Date();
const dateString = d.toISOString();
const dateStringSub = dateString.substring(0, 10);

export default {
  props: ['item'],
  setup() {
    return {
      name: ref(''),
      invoice: ref(''),
      paid: ref(''),
      receipt: ref(''),
      date: ref(dateStringSub),
      prompt: ref(false),
    };
  },
  methods: {
    triggerDialogue() {
      this.name = this.item[0].name;
      this.invoice = this.item[0].invoice;
      this.paid = this.item[0].paid;
      this.receipt = this.item[0].receipt;
      this.date = this.item[0].date;
      this.prompt = true;
    },
    nextInput(i) {
      switch (i) {
        case 1:
          this.$refs.invoiceInput.focus();
          break;
        case 2:
          this.$refs.amountInput.focus();
          break;
        case 3:
          this.$refs.receiptInput.focus();
          break;
        case 4:
          this.$refs.dateProxy.show();
          break;
      }
    },
    submitTransaction() {
      const updatedTransaction = {
        name: this.name,
        invoice: this.invoice,
        paid: this.paid,
        receipt: this.receipt,
        date: this.date,
      };
      console.log('Submitting: ', JSON.stringify(updatedTransaction));
      // send request to server with fields
    },
    cancelTransaction() {
      this.prompt = false;
    },
  },
};
</script>
