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
    <button v-if="!isEditing" @click="onEdit" class="edit-btn">編輯</button>
    <button v-if="!isEditing" @click="onDelete" class="delete-btn">刪除</button>
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

<style scoped>
.edit-btn {
  background: #fff;
  color: #222;
  border: 1px solid #222;
  border-radius: 4px;
  padding: 2px 10px;
  margin-left: 8px;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.edit-btn:hover {
  background: #222;
  color: #fff;
}
.delete-btn {
  background: #e53935;
  color: #fff;
  border: 1px solid #e53935;
  border-radius: 4px;
  padding: 2px 10px;
  margin-left: 8px;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.delete-btn:hover {
  background: #b71c1c;
  border-color: #b71c1c;
}
</style>
