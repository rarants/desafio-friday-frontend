<template>
  <div class="card mt-2">
    <div class="grid grid-cols-2 gap-3 mb-4">
      <div class="col-span-1 mb-2">
        <TransactionField label="Account" :value="trx.account.name" />
      </div>
      <div class="col-span-1 mb-2">
        <TransactionField label="Bank" :value="trx.account.bank" />
      </div>
      <div class="col-span-1 mb-2">
        <TransactionField label="Transaction date" :value="trx.date" />
      </div>
      <div class="col-span-1 mb-2">
        <TransactionField
          label="Reference"
          :value="trx.reference ? trx.reference : 'No reference provided'"
        />
      </div>
      <div class="col-span-1 mb-2">
        <TransactionField
          label="Category"
          :value="trx.category.name"
          :color="trx.category.color"
        />
      </div>
      <div class="col-span-1 mb-2">
        <TransactionField
          label="Amount"
          :value="trx.amount"
          :currency="trx.currency"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Transaction",
  data() {
    return {
      trx: {
        id: "12d73b77-208a-443e-9231-88831520280b",
        accountId: "c5f3f93c-bf33-402e-a9f1-c15c148d451b",
        categoryId: "a5f851cb-f3ff-41e3-8629-929395e65d50",
        reference: "",
        amount: "-77.07",
        currency: "EUR",
        date: "2018-02-04 09:07:21.000",
        account: {
          id: "c5f3f93c-bf33-402e-a9f1-c15c148d451b",
          name: "Anonymous",
          bank: "iBank",
        },
        category: {
          id: "a5f851cb-f3ff-41e3-8629-929395e65d50",
          name: "Vendors",
          color: "ff6955",
        },
      },
    };
  },
};
</script>
