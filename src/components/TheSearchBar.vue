<template>
    <div>
        <input @keyup.enter="onInputKeyword" type="text">
    </div>
</template>

<script>
export default {
  methods: {
      onInputKeyword : function (event){
          this.$emit('input-change', event.target.value)
      }
  }
}
</script>


