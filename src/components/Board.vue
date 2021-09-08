<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem :game-status="gameStatus" v-for="field in fields" :field="field" :key="'item-' + field.id"
                 @selectField="selectField($event)"
      />

      <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>
      <div class="result">
        <div class="win" v-if="isWin">Поздравляем! Продолжаем играть!
          <div class="win__img"><img src="../assets/images/smile-joy.svg" alt="smile-joy"></div>
        </div>
        <div class="fail" v-if="isFail">Вы проиграли. Попробуйте еще раз!
          <div class="win__img"><img class="win__img" src="../assets/images/smile-sad.svg" alt="smile-sad"></div>
        </div>
      </div>
      <button class="btn" @click="start" :disabled="!canStartGame">Старт</button>
    </div>
  </div>

</template>

<script>
import BoardItem from './BoardItem.vue'
import {onBeforeMount, ref} from 'vue'
import useGameInit from './composables/useGameInit'
import useGameStart from './composables/useGameStart'
import {GAME_STATUS} from '../constants'
import useGameProcess from './composables/useGameProcess'

export default {
  name: 'Board',
  components: {BoardItem},

  setup() {
    const number = 25
    const gameStatus = ref(GAME_STATUS.NONE)

    const {difficult, fields, init} = useGameInit(number)
    const {start, canStartGame} = useGameStart(init, fields, difficult, number, gameStatus)
    const {selectField, isWin, isFail} = useGameProcess(fields, gameStatus, difficult, start)

    return {
      difficult,
      fields,
      number,
      init,
      start,
      gameStatus,
      canStartGame,
      selectField,
      isWin,
      isFail
    }
  },
  methods: {}
}
</script>

<style scoped>
.board-wrapper {
  margin-bottom: 3rem;
}

.board {
  width: 300px;
  background: #eee;
  padding: .5rem 0;
  margin: 0 auto;
  font-weight: bold;
}

.btn {
  background: cadetblue;
  color: white;
  border: none;
  border-radius: .5rem;
  padding: .8rem 1.5rem;
  font-weight: bold;
  font-size: 1rem;
  outline: none;
}

.btn:hover {
  background: lightslategrey;
}

.btn:active {
  transform: scale(.9);
  background: cadetblue;
  color: palegoldenrod;
}

.btn:disabled {
  opacity: .5;
}

.result {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: nowrap;
}

.win {
  color: seagreen;
}

.fail {
  color: firebrick;
}

.win__img {
  align-self: flex-end;
  display: flex;
  width: 50px;
  background: transparent;
}
</style>