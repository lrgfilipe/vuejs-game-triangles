<template>
  <div :class="type" @click="$emit('click')" />
</template>

<script>
export default {
  props: {
    type: { type: String, required: true }
  }
}
</script>

<style>
.up {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 75px solid #555;
}
.down {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-top: 75px solid #555;
}
.left {
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-right: 75px solid #555;
  border-bottom: 50px solid transparent;
}
.right {
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-left: 75px solid #555;
  border-bottom: 50px solid transparent;
}
</style>
