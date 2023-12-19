<template>
  <div class="relative" @click="isOpen = !isOpen">
    <label class="text-gray-600">Select</label>
    <div
      class="relative mt-1 z-50"
      :class="{
        'multi-select': type === 'multi',
        'single-select': type === 'single',
      }"
    >
      <button
        class="w-full flex items-center justify-between px-4 py-2 text-sm leading-5 rounded-md focus:outline-none focus:shadow-outline-blue transition ease-in-out duration-150"
        :class="{
          'border-blue-500 bg-blue-100': isOpen,
          'border-gray-300 bg-gray-100': !isOpen,
        }"
      >
        {{ selectedModel || "Select" }}
        <svg
          class="w-5 h-5 ml-2"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 9l-7 7-7-7"
          ></path>
        </svg>
      </button>
      <transition name="fade">
        <ul
          v-show="isOpen"
          class="absolute left-0 mt-2 w-full bg-white border shadow-md rounded-md overflow-hidden z-100 relative"
        >
          <slot name="header"></slot>

          <li
            v-for="option in options"
            :key="option.value"
            @click="toggleSelect(option)"
            class="block px-4 py-2 text-sm leading-5 text-gray-800 cursor-pointer hover:bg-gray-100"
            :class="{
              'cursor-not-allowed opacity-50': option.disabled,
              'hover:bg-gray-100': !option.disabled && !isSelected(option),
              'font-bold bg-blue-100': isSelected(option),
            }"
          >
            <slot :name="`option-${option.name}`">
              {{ option?.[optionKey] ?? option }}
            </slot>
          </li>

          <slot name="footer"></slot>
        </ul>
      </transition>
    </div>
  </div>
</template>

<script setup>
import vClickOutside from "click-outside-vue3";
import { computed, ref } from "vue";

const isOpen = ref(false);
const props = defineProps({
  type: {
    type: String,
    default: "single",
  },
  options: {
    type: Array,
    default: () => [],
    required: true,
  },
  modelValue: {
    type: [String, Number, Array, Object, null],
    default: () => "",
  },
  optionKey: {
    type: String,
    default: "label",
  },
  optionValue: {
    type: String,
    default: "value",
  },
});

const emits = defineEmits(["update:modelValue"]);

const model = computed({
  get() {
    return props.modelValue;
  },
  set(val) {
    emits("update:modelValue", val);
  },
});

const selectedModel = computed(() => {
  return Array.isArray(model.value) ? model.value?.join(",") : model.value;
});

//checking option type

function toggleSelect(option) {
  if (option.disabled) {
    return; // Do nothing if the option is disabled
  }

  if (props.type === "single") {
    console.log(props.type);
    console.log("Ho");
    model.value = getOptionValue(option); // For single-select, replace the array with a single value
  } else {
    if (isSelected(option)) {
      model.value = model.value.filter(
        (item) => item !== getOptionValue(option)
      );
    } else {
      model.value.push(getOptionValue(option));
    }
  }
}

function getOptionValue(option) {
  // Check if the option is an object with a 'value' property
  return typeof option === "object" && option.hasOwnProperty(props.optionValue)
    ? option[props.optionValue]
    : option;
}

function isSelected(option) {
  return model.value.includes(getOptionValue(option));
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
