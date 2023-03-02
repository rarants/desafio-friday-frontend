<template>
  <table class="border-collapse table-auto w-full text-sm">
    <thead>
      <tr>
        <th class="text-left">Reference</th>
        <th class="text-left">Category</th>
        <th class="text-left">Date</th>
        <th class="text-left">Amount</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="(trx, index) in transactions.data"
        :key="index"
        class="odd:bg-white even:bg-slate-50 hover:bg-slate-100 hover:cursor-pointer"
        @click="$router.push(`transactions/${trx.id}`)"
        title="Click to view more details"
        
      >
        <td class="py-3 pl-2">
          {{ trx.reference || 'No reference provided' }}
        </td>
        <td>
          <span
            class="badge"
            :style="
              trx.category.color !== ''
                ? { 'background-color': '#' + trx.category.color }
                : { 'background-color': '#D0D0D0' }
            "
            v-if="trx.category"
          >
            {{ trx.category.name }}
          </span>
          <span v-else>No category provided</span>
        </td>
        <td>{{ $moment(trx.date).format('D/MM/YYYY') }}</td>
        <td>
          {{ trx.amount }}
          <span
            class="font-medium"
            :class="{
              'text-red-500': trx.amount < 0,
              'text-green-500': trx.amount > 0,
            }"
          >
            {{ trx.currency }}
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'TransactionsTable',
  props: {
    model: {
      required: true,
      value: Object,
    },
  },
  data() {
    return {
      transactions: [],
    }
  },
  async mounted() {
    await this.loadTransactions()
  },
  methods: {
    async loadTransactions() {
      const filters = this.formatFilters()
      try {
        const { data } = await this.$axios.get(`/transactions${filters}`)
        this.transactions = data;
      } catch (e) {
        console.log(e)
      }
    },
    formatFilters() {
      let filters = ''
      const model = this.model
      if (model.text) filters += `?text=${model.text}`

      if (model.bank) {
        filters ? filters += "&" : filters += "?";
        filters += `bank=${model.bank}`
      }
      if (model.account) {
        filters ? filters += "&" : filters += "?";
        filters += `account=${model.account}`
      }
      if (model.start_month) {
        filters ? filters += "&" : filters += "?";
        filters += `start_month=${model.start_month}`
      }
      if (model.end_month) {
        filters ? filters += "&" : filters += "?";
        filters += `end_month=${model.end_month}`
      }
      return filters
    },
  },
  watch: {
    'model.text': async function () {
      setTimeout(this.loadTransactions.bind(this), 1500)
    },
    'model.bank': async function () {
      await this.loadTransactions()
    },
    'model.account': async function () {
      await this.loadTransactions()
    },
    'model.start_month': async function () {
      await this.loadTransactions()
    },
    'model.end_month': async function () {
      await this.loadTransactions()
    },
  },
}
</script>
