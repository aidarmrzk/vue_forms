<template>
  <div>
    <p>{{ label }}</p>
    <select @change="updateSelect">
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
        :selected="option.selected"
      >{{ option.text }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "FormSelect",

  props: {
    label: {
      type: String,
      default: ''
    },

    options: {
      type: Object,
      required: true
    },
  },
  methods: {
    updateSelect(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  },
  mounted() {
    const selectedOption = this.options.find(option => option.selected);
    if (!selectedOption) {
      if (this.options.length > 0) {
        this.options[0].selected = true;
        this.$emit('update:modelValue', this.options[0].value);
      }
    } else {
      this.$emit('update:modelValue', selectedOption.value);
    }
  },
}
</script>

<style scoped lang="scss">
p {
  margin: 0 0 5px 10px;
}
select {
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  border: none;
  font-size: 16px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background: url("@/assets/img/expand-arrow.png") no-repeat right center;
  background-size: 14px 14px;
  background-position: right 10px center;
  background-color: #fff;
  cursor: pointer;

  &:focus {
      border-color: rgb(155, 63, 212);
      box-shadow: 0 0 0 0.25rem rgba(163, 70, 244, 0.3);
  }
  option {
      cursor: pointer;
  }
}
</style>
