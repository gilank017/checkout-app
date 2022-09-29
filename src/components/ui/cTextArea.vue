<template>
  <div class="form-floating">
    <textarea class="form-control" :class="className" :placeholder="placeholder" :id="forId" @input="updateValue" :value="modelValue" maxlength="120" style="height: 120px"></textarea>
    <label :for="forId">{{ label }}</label>
    <span class="counter-text">{{ total }}</span>
  </div>
</template>
<script>
import { computed } from '@vue/runtime-core'
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
    label: {
      type: String,
      required: true
    },
    placeholder: {
      type: String,
      required: true
    },
    modelValue: {
      type: String,
      default: ''
    }
  },
  setup(props, context) {

    const total = computed(() => {
      return 120 - Object.values(props.modelValue).length
    })

    function updateValue(event) {
      context.emit("update:modelValue", event.target.value)
    }
    return {
      updateValue,
      total
    }
  }
}
</script>
<style lang="stylus">
.counter-text
  background-color #ff8a00
  color #fff
  font-weight bold
  font-size 12px
  padding 8px 0px
  border-radius 50%
  position absolute
  right -15px
  bottom -15px
  height 33px
  width 35px
</style>