<template>
  <div class="form-floating mb-3">
    <input :type="type" class="form-control" :class="className" :id="forId" :placeholder="placeholder" @input="updateValue" :value="modelValue">
    <label :for="forId">{{ label }}</label>
  </div>
</template>
<script>
export default {
  props: {
    forId: {
      type: String,
      required: true
    },
    className: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    label: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    modelValue: {
      type: [String, Number],
      default: ''
    }
  },
  setup(props, context) {
    function updateValue(event) {
      context.emit("update:modelValue", event.target.value)
    }
    return {
      updateValue
    }
  }
}
</script>
<style lang="stylus">
.form-control.is-invalid, .was-validated .form-control:invalid
  border-color #FF8A00 !important
</style>