<script setup>
import { ref } from "vue";
import ISelect from "./components/ISelect.vue";
import CodeSelect from "./components/CodeSelect.vue";
const options = ref(["Option1", "Option2", "Option3"]);
const optonsWithLabelValue = ref([
  {
    label: "India",
    value: "India",
  },
  {
    label: "Usa",
    value: "Usa",
  },
]);
const optionsWithDisabled = ref([
  {
    label: "India",
    value: "India",
    disabled: true,
  },
  {
    label: "Usa",
    value: "Usa",
    disabled: false,
  },
]);

const select = ref("");
const multSelect = ref([]);
const singleOption = ref("");
const multiOption = ref([]);

const optionsWithDifferentKeyValue = ref([
  {
    name: "Yasin",
    age: 28,
  },
  {
    name: "Albert",
    age: 30,
  },
]);
const optionSlotItem = ref([
  {
    label: "Yasin",
    value: 28,
    name: "yasin",
  },
  {
    label: "Albert",
    value: 30,
    name: "albert",
  },
]);
</script>

<template>
  <section class="p-20">
    <div class>
      <a
        href="https://github1s.com/yasin7044/invelo-select"
        class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
        >Code Link
      </a>
      <p></p>
      <b>ISelect.vue</b> <code>src/components/ISelect.vue</code>
      <div>
        is the component for a select component that handles a 1D array, an
        array of objects, dynamic key-value pairs, and also slots.
      </div>
    </div>
    <CodeSelect
      :select="select"
      :options="options"
      class="my-4"
      title="Example1: Single Select - Options without label and value (1D array)"
    >
      <ISelect v-model="select" :options="options" />
    </CodeSelect>
    <CodeSelect
      :select="multSelect"
      :options="options"
      class="my-4"
      title="Example2: Multi Select - Options without label and value (1D array) - Passing type multi"
    >
      <ISelect v-model="multSelect" :options="options" type="multi" />
    </CodeSelect>

    <CodeSelect
      :select="singleOption"
      :options="optonsWithLabelValue"
      class="my-4"
      type="multi"
      title="Example3: Single Select - Options without label and value"
    >
      <ISelect v-model="singleOption" :options="optonsWithLabelValue" />
    </CodeSelect>

    <CodeSelect
      :select="multiOption"
      :options="optonsWithLabelValue"
      class="my-4"
      type="multi"
      title="Example4: Multi Select - Options without label and value"
    >
      <ISelect
        v-model="multiOption"
        :options="optonsWithLabelValue"
        type="multi"
      />
    </CodeSelect>

    <CodeSelect
      :select="multiOption"
      :options="optionsWithDifferentKeyValue"
      class="my-4"
      type="multi"
      title="Example4:  Select - options WithDifferent KeyValue we need to pass optionKey and optionValue as a string"
    >
      <ISelect
        v-model="multiOption"
        :options="optionsWithDifferentKeyValue"
        type="multi"
        optionKey="name"
        optionValue="age"
      />
    </CodeSelect>

    <CodeSelect
      :select="multiOption"
      :options="optionsWithDifferentKeyValue"
      class="my-4"
      type="multi"
      title="Example5:  Select - options Slot header footer"
    >
      <ISelect
        v-model="multiOption"
        :options="optionsWithDifferentKeyValue"
        type="multi"
        optionKey="name"
        optionValue="age"
      >
        <template #header>
          <li
            class="block px-4 py-2 text-sm leading-5 text-gray-800 cursor-pointer hover:bg-gray-100"
            @click.stop
          >
            hi I am header slot
          </li>
        </template>

        <template #footer>
          <li
            class="block px-4 py-2 text-sm leading-5 text-gray-800 cursor-pointer hover:bg-gray-100"
            @click.stop
          >
            hi I am Footer slot Load More (example)
          </li>
        </template>
      </ISelect>
    </CodeSelect>
  </section>
</template>
