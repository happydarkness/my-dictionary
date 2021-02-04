<template>
  <div id="wrap-new-word">
    <div class="new-word">
      <form action="" class="new-word-form">
        <label for="word"></label>
        <input type="text" class="word" id="word">
        <label for="translate"></label>
        <input type="text" class="translate" id="translate">
        <button class="submit-word">Save</button></form>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="sass">
/** body для того чтобы не было прокрутки но там вылазят бока которые надо пофиксить
  overflow: hidden
  overflow-x: hidden
  overflow-y: hidden **/

#wrap-new-word
  position: fixed
  top: 0
  left: 0
  z-index: 10000
  width: 100%
  height: 100%
  background: rgba($main-dark-text-color, 0.5)
  

</style>