<template>
  <div>
    <textarea
      v-model="selectedValue"
      :placeholder="$attrs['placeholder']"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>

<script setup>
import { useFormField } from "../../../composables/useFormField";

defineEmits(["update:modelValue"]);

const props = defineProps({
  field: {
    type: Object,
    default: null,
  },
  modelValue: {
    type: String,
    default: "",
  },
  // type: {
  //   type: String,
  //   default: "textarea",
  // },
  // name: {
  //   type: String,
  //   default: null,
  // },
  // validation: {
  //   type: Object,
  //   default: null,
  // },
});

const { selectedValue } = useFormField(props);
</script>
