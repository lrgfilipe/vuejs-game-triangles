<template>
  <div>
    <div class="border-b-2 border-white flex pb-4">
      <div class="w-1/2 flex items-center justify-center font-medium text-2xl text-white">
        App Name
      </div>
      <div class="w-1/2 text-center font-medium text-white rounded-lg text-lg bg-orange-500">
        <div class="border-b border-white py-1">
          Score: {{ score }}
        </div>
        <div class="py-1">
          High Score: {{ highScore }}
        </div>
      </div>
    </div>
    <board @score="setScore" />
  </div>
</template>

<script>
import Board from '~/components/Board.vue'
export default {
  components: { Board },
  data () {
    return {
      score: 0,
      highScore: 0
    }
  },
  mounted () {
    this.highScore = localStorage.getItem('highScore') || 0
  },
  methods: {
    setScore (event) {
      this.score = event
      if (this.score > this.highScore) {
        this.highScore = this.score
        localStorage.setItem('highScore', this.highScore)
      }
    }
  }
}
</script>
