<template>
  <form @submit.prevent="onSave">
    <input type="text" v-model.trim="editValue" />
    <button type="submit">儲存</button>
    <button type="button" @click="onCancel">取消</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
const props = defineProps({
  modelValue: {
    type: String,
    required: true
  }
})
const emit = defineEmits(['save', 'cancel'])
const editValue = ref(props.modelValue)

function onSave() {
  emit('save', editValue.value)
}
function onCancel() {
  emit('cancel')
}
</script>

