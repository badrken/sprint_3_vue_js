<template>
  <div :class="`alert alert-${status}`" role="alert">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ['status'],
}
</script>

<style>

</style>