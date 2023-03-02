<template>
  <div class="card overflow-x-auto">
    <div class="grid grid-cols-10 gap-3 mb-4">
      <div class="col-span-10 md:col-span-4 mb-2">
        <label class="relative block">
          <span class="text-sm font-medium text-slate-700"> Search </span>
          <input
            type="text"
            name="search"
            class="mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 w-full rounded-md"
            placeholder="Search by bank, account, reference, category, date, amout, currency..."
            v-model="model.text"
          />
        </label>
      </div>
      <div class="col-span-10 md:col-span-1 mb-2">
        <label
          for="bank"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Bank</label
        >
        <select
          id="bank"
          class="bg-white border border-gray-300 shadow-sm text-gray-900 text-sm rounded-md focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          v-model="model.bank"
        >
          <option value="" selected>No filter applied</option>
          <option
            v-for="(bank, idx) in banks"
            :key="'bank_' + idx"
            :value="bank.bank"
          >
            {{ bank.bank }}
          </option>
        </select>
      </div>
      <div class="col-span-10 md:col-span-1 mb-2">
        <label
          for="account"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Account</label
        >
        <select
          id="account"
          class="bg-white border border-gray-300 shadow-sm text-gray-900 text-sm rounded-md focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          v-model="model.account"
        >
          <option value="" selected>No filter applied</option>
          <option
            v-for="(acc, idx) in accounts"
            :key="'acc_' + idx"
            :value="acc.name"
          >
            {{ acc.name }}
          </option>
        </select>
      </div>
      <div class="col-span-10 md:col-span-2 mb-2">
        <label for="start_month" class="relative block">
          <span class="text-sm font-medium text-slate-700">
            Starting month
          </span>
          <input
            type="month"
            id="start_month"
            name="start_month"
            min="1980-01"
            value=""
            v-model="model.start_month"
            class="bg-white border border-gray-300 shadow-sm text-gray-900 text-sm rounded-md focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          />
        </label>
      </div>
      <div class="col-span-10 md:col-span-2 mb-2">
        <label for="end_month" class="relative block">
          <span class="text-sm font-medium text-slate-700"> Ending month </span>
          <input
            type="month"
            id="end_month"
            name="end_month"
            min="1980-01"
            value=""
            v-model="model.end_month"
            class="bg-white border border-gray-300 shadow-sm text-gray-900 text-sm rounded-md focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          />
        </label>
      </div>
    </div>
    <TransactionsTable :model="model" />
  </div>
</template>

<script>
export default {
  name: 'Transactions',
  data() {
    return {
      model: {
        text: '',
        bank: '',
        account: '',
        start_month: '',
        end_month: '',
      },
      mounths: [
        {
          mounth: 1,
          name: 'January',
        },
        {
          mounth: 2,
          name: 'February',
        },
        {
          mounth: 3,
          name: 'March',
        },
        {
          mounth: 4,
          name: 'April',
        },
        {
          mounth: 5,
          name: 'May',
        },
        {
          mounth: 6,
          name: 'June',
        },
        {
          mounth: 7,
          name: 'July',
        },
        {
          mounth: 8,
          name: 'August',
        },
        {
          mounth: 9,
          name: 'September',
        },
        {
          mounth: 10,
          name: 'October',
        },
        {
          mounth: 11,
          name: 'November',
        },
        {
          mounth: 12,
          name: 'December',
        },
      ],
      accounts: [],
      categories: [],
      banks: [],
    }
  },
  async mounted() {
    await this.loadFields('accounts')
    await this.loadFields('categories')
    await this.loadFields('banks')
  },
  methods: {
    async loadFields(field) {
      try {
        const { data } = await this.$axios.get(`/${field}`)
        this[field] = data
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>
