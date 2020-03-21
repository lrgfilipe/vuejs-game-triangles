<template>
  <div>
    <div
      class="h-32 text-2xl text-center font-bold text-gray-700 flex flex-col justify-center cursor-pointer"
      @click="start()"
    >
      {{ nextPlay }}
      <div v-if="gameOver">
        GAME OVER !
      </div>
    </div>
    <progress-bar
      size="large"
      :val="clock"
      :max="totalClock"
      class="mb-10 border-2 border-white rounded-full"
      bg-color="transparent"
      :bar-border-radius="100"
      bar-color="#ed8936"
    />
    <div class="flex flex-wrap">
      <div
        v-for="(item, index) in board"
        :key="index"
        class="w-1/2"
        :class="[index % 2 === 0 ? 'border-r-2 pr-4' : 'pl-4']"
      >
        <div
          class="h-32 flex items-center justify-center"
          :class="[index < 2 ? 'border-b-2 ' : '']"
        >
          <triangle
            :type="item"
            class="cursor-pointer"
            @click="userPlay(item)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProgressBar from 'vue-simple-progress'
import _ from 'lodash'
import Triangle from '~/components/Triangle.vue'
export default {
  components: { Triangle, ProgressBar },
  data () {
    return {
      board: ['up', 'down', 'left', 'right'],
      nextPlay: 'TAP HERE TO START ...',
      interval: null,
      totalClock: 2000,
      clock: 2000,
      score: 0,
      highScore: 0,
      gameOver: false,
      inGame: false
    }
  },
  methods: {
    getGame () {
      const possible = ['up', 'down', 'left', 'right']

      // next play
      this.nextPlay = _.chain(possible).clone().filter(item => item !== this.nextPlay).sample().value()
      this.board = []

      let i
      for (i = 0; i < 4; i++) {
        const item = _.sample(possible)
        _.remove(possible, i => i === item)
        this.board.push(item)
      }

      this.startClock()
    },
    startClock () {
      this.clock = this.totalClock
      clearInterval(this.interval)
      this.interval = setInterval(() => {
        this.clock -= 200
        if (this.clock < 0) {
          this.endGame()
        }
      }, 200)
    },
    userPlay (item) {
      if (!_.isEqual(item, this.nextPlay)) {
        this.endGame()
      } else {
        this.changeScore(this.score + 1)
        this.$emit('score', this.score)
        this.getGame()
      }
    },
    start () {
      if (!this.inGame) {
        this.inGame = true
        this.clock = this.totalClock
        this.gameOver = false
        this.changeScore(0)
        setTimeout(() => {
          this.getGame()
        }, 500)
      }
    },
    changeScore (val) {
      this.score = val
      this.$emit('score', val)
    },
    endGame () {
      this.inGame = false
      clearInterval(this.interval)
      this.gameOver = true
      this.nextPlay = 'TAP HERE TO START ...'
    }
  }
}
</script>
