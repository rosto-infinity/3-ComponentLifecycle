<template>

 
  <label>
    <input type="checkbox" @change="onChange"/>{{ label }}
  </label>


</template>

<script setup>
import { ref } from 'vue';
const props = defineProps({
label: String,
});

const emits =defineEmits(['check', 'uncheck']);
const onChange = (event) => {
if (event.target.checked) {
  emits('check');
} else {
  emits('uncheck');
}
};

</script>
