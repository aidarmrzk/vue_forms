<template>
  <div>
    <p>{{ label }}</p>
    <input
        v-bind="$attrs"
        :type="type"
        @input="updateInput"
        required
    />
  </div>
</template>

<script>
export default {
  name: "FormInput",

  props: {
    label: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  },
}
</script>

<style scoped>
p {
  margin: 0 0 5px 10px;
}
input {
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  border: none;
  font-size: 16px;
}
</style>
