<template>
  <div>
    <div class="border-b-2 border-white flex pb-4">
      <div class="w-1/2 flex items-center justify-center border-r-2 border-white font-medium text-2xl text-white ">
        App Name
      </div>
      <div class="w-1/2 text-right">
        <div>Score: </div>
        <div>High Score: </div>
      </div>
    </div>
    <board />
  </div>
</template>

<script>
import Board from '~/components/Board.vue'
export default {
  components: { Board }
}
</script>
