<template>
  <div class="form-floating">
    <input :type="type" class="form-control" :class="className" :id="forId" :placeholder="placeholder" @input="updateValue" :value="modelValue">
    <label :for="forId">{{ label }}</label>
  </div>
  <div v-if="className === 'is-invalid'" class="error-message">{{ message }}</div>
  
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
    },
    message: {
      type: String,
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
.form-control.is-valid, .was-validated .form-control:valid
  border-color #1BD97B !important
.error-message
  font-size .875em
  color #FF8A00
  text-align left
</style>