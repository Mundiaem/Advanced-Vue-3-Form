<template>
  <div class='tag-input'>
    <select class="form-control" v-model="selectedValue" @change="$emit('update:modelValue', selectedValue)"
            :placeholder="$attrs['placeholder']"
    >
      <option value="">Select One</option>
      <option v-for="(option, key) in props.field.options.choices"
              :id="option"
              :key="key"
              :value="option"
              @input="$emit('update:modelValue', selectedValue)"
      >
        {{ option }}
      </option>
    </select>

  </div>
</template>

<script setup>
import {useFormField} from "../../../composables/useFormField";

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
  //   default: null,
  // },
  // options: {
  //   type: Array,
  //   default: () => [],
  // },
  // name: {
  //   type: String,
  //   default: "",
  // },
  // validation: {
  //   type: Object,
  //   default: null,
  // },
});

const {selectedValue} = useFormField(props);
</script>
