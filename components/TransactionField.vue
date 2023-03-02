<template>
  <div>
    <label class="relative block mb-1">
      <span class="text-sm font-medium text-slate-700">{{ label }}</span>
    </label>
    
    <div v-if="type && type === 'input-text'">
      <input
        type="text"
        :name="label"
        class="mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 w-full rounded-md"
        :placeholder="placeholder"
      />
    </div>
    <div v-if="type && type === 'input-date'"></div>
    <div v-if="type && type === 'input-select'"></div>
    <span
      v-if="label === 'Category'"
      class="badge"
      :style="
        color
          ? { 'background-color': '#' + color }
          : { 'background-color': '#D0D0D0' }
      "
    >
      {{ value }}
    </span>
    <div v-else-if="label === 'Amount'">
      {{ value }}
      <span
        class="font-medium"
        :class="{
          'text-red-500': value < 0,
          'text-green-500': value > 0,
        }"
      >
        {{ currency }}
      </span>
    </div>
    <span v-else>{{ value }}</span>
  </div>
</template>

<script>
export default {
  name: "Transaction",
  props: {
    label: {
      required: true,
      value: String,
    },
    value: {
      required: true,
      value: String,
    },
    type: {
      required: false,
      value: ["input-text", "input-date", "input-select"],
    },
    color: {
      required: false,
      value: String,
    },
    currency: {
      required: false,
      value: String,
    },
  },
};
</script>
