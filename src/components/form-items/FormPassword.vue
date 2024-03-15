<template>
  <FormInput :label="label" :type="type" />
</template>

<script>
import FormInput from "@/components/form-items/FormInput.vue";

export default {
  name: "FormPassword",
  props: {
    label: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'password'
    }
  },
  components: {
    FormInput
  }
}
</script>

<style lang="scss" scoped>

</style>
