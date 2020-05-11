<template>
  <div class="box">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>
</template>

<script>
export default {
  
}
</script>

<style lang="stylus" scoped>
  * 
    padding 0
    margin 0

  .box
    width 100%
    height 200px
    background-color #ccc
  
  .box > div
    width 100%
    height 100%
    background-color skyblue
    box-sizing border-box
    border-right 2px solid blue
    border-bottom 2px solid blue
    float left

  @media screen and (min-width 768px)
    .box > div
      width 50%

  @media screen and (min-width 992px)
    .box > div
      width 33.33%
  
  @media screen and (min-width 1200px)
    .box > div
      width 25%
</style>