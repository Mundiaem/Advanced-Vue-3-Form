<template>
  <div class='tag-input'>
    <div v-for='(tag, index) in props.modelValue' :key='index' class='tag-input__tag'>
      <span @click='removeTag(index)'>x</span>
      {{ tag }}
    </div>
    <input
        class='tag-input__text'
        :id="props.field.name"
        :type="props.field.type"
        :name="props.field.name"
        :placeholder="$attrs['placeholder']"
        @keydown.enter="addTag"
        @keydown.188="addTag"
        @change="$emit('update:modelValue',  props.modelValue)"
    /></div>

</template>

<script setup>
import {useFormField} from "../../../composables/useFormField";
import {getCurrentInstance} from "vue";

defineEmits(["update:modelValue"]);

const props = defineProps({
  field: {
    type: Object,
    default: null,
  },
  modelValue: {
    type: Array,
    default: () => [],
  },

  // type: {
  //   type: String,
  //   default: null,
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
const instance = getCurrentInstance();


function addTag(event) {
  event.preventDefault()
  var val = event.target.value.trim()
  if (val.length > 0) {
    props.modelValue.push(val)
    event.target.value = ''
    instance?.proxy?.$forceUpdate();
  }
  // console.log("Tag: ", val, " --- ", props.modelValue)
}

function removeTag(index) {
  props.modelValue.splice(index, 1)
instance?.proxy?.$forceUpdate();
}

const {selectedValue, vFocus} = useFormField(props);
</script>
