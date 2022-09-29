<template>
  <div class="progressbar-wrapper">
    <ul class="progressbar p-0">
      <li class="active">Delivery</li>
      <i class="fa fa-chevron-right icon-arrow-1" aria-hidden="true"></i>
      <li>Payment</li>
      <i class="fa fa-chevron-right icon-arrow-2" aria-hidden="true"></i>
      <li>Finish</li>
    </ul>
  </div>
</template>
<style lang="stylus" scoped>
.progressbar-wrapper
  width 40%
  position absolute
  z-index 1
  left 50%
  transform translateX(-50%)
  top 50px
  background-color #FFFAE6
  border-radius 40px
  height 40px
  border-bottom 1px solid #0000002d
  .progressbar
    counter-reset step
  .progressbar li
    float left
    width 33.3%
    position relative
    text-align center
    list-style none
    color #FF8A00
    font-weight bold
    &:before
      content counter(step)
      counter-increment step
      width 30px
      height 30px
      border 2px solid #FF8A00
      display inline-block
      margin 0 10px
      border-radius 50%
      line-height 27px
      background transparent
      color #FF8A00
      text-align center
      font-weight bold
  li.active
    &:before
      border-color #FF8A00
      background #FF8A00
      color #fff
    &:after
      background #FF8A00
  .icon-arrow-1
    color #FF8A00
    position absolute
    left 220px
    top 8px
  .icon-arrow-2
    color #FF8A00
    position absolute
    right 210px
    top 8px
</style>