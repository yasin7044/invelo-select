<template>
  <div class="bg-red-100 p-6">
    <h3 class="text-h3 my-4">
      {{ title }}
    </h3>
    <code>
      const options =
      <span class="bg-red-100 p-2">
        <pre>{{ options }}</pre>
      </span>
      <span class="bg-orange-100 ml-10 p-2">v-model = {{ select }}</span>
    </code>

    <slot></slot>
  </div>
</template>

<script setup>
defineProps({
  options: {
    type: Array,
    required: true,
    default: () => [],
  },
  select: {},
  title: {
    type: String,
    default: "",
  },
});
</script>

<style lang="scss" scoped></style>
