<template>
  <div>
    <input
      type="checkbox"
      :id="id"
      :checked="isDone"
      @change="onCheck"
    />
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
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
      isDone: this.done
    };
  },
  methods: {
    onCheck(event) {
      this.isDone = event.target.checked;
      this.$emit('change', { id: this.id, done: this.isDone });
    }
  }
};
</script>
