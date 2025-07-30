<!--使用者從這裡勾選清單，透過「事件」把資料傳過去App.vue-->

<template>
  <div>
    <input
      type="checkbox"
      :id="id"
      :checked="isDone"
      @change="onCheck"
      :disabled="isEditing"
    />
    <label :for="id" v-if="!isEditing">{{ label }}</label>
    <button v-if="!isEditing" @click="onEdit">編輯</button>
    <button v-if="!isEditing" @click="onDelete">刪除</button>
    <ToDoItemEditForm
      v-if="isEditing"
      :modelValue="label"
      @save="onEditSave"
      @cancel="onEditCancel"
    />
  </div>
</template>

<script>
import ToDoItemEditForm from './ToDoItemEditForm.vue'
export default {
  name: 'TodoItem',
  components: { ToDoItemEditForm },
  props: {
    label: {
      type: String,
      required: true
    },
    done: {
      type: Boolean,
      default: false
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      isDone: this.done,
      isEditing: false
    };
  },
  watch: {
    done(val) {
      this.isDone = val;
    }
  },
  methods: {
    onCheck(event) {
      this.isDone = event.target.checked;
      this.$emit('change', { id: this.id, done: this.isDone });
    },
    onEdit() {
      this.isEditing = true;
    },
    onDelete() {
      this.$emit('delete', this.id);
    },
    onEditSave(newLabel) {
      this.$emit('edit', { id: this.id, label: newLabel });
      this.isEditing = false;
    },
    onEditCancel() {
      this.isEditing = false;
    }
  }
};
</script>
