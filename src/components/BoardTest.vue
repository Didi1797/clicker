<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem :game-status="gameStatus" v-for="field in fields" :field="field" :key="'item-' + field.id" 
        @selectField="selectField($event)"/>
    </div>
    
    <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>
    <p class="win" v-if="isWin"> <strong>Финаминальная память! Попробуй сложность повыше!</strong></p>
    <p class="fail" v-if="isFail"><strong>Не расстраивайся! В следующий раз получится! =)</strong></p>
  
    <button class="btn" @click="start" :disabled="!canStartGame">Старт</button>
  </div>
</template>

<script>
import BoardItem from './BoardItem';
import useGameInit from '@/components/composables/useGameInit';
import useGameStart from '@/components/composables/useGameStart';
import useGameProcess from '@/components/composables/useGameProcess'
import { GAME_STATUS } from '@/constants';
import { ref } from 'vue'

export default {
  name: 'BoardTest',
  props: {},
  components: {
    BoardItem,
  },
  setup() {
    const number = 25;
    const gameStatus = ref(GAME_STATUS.NONE);
    
    const { difficult, fields, init } = useGameInit(number);

    const { start, canStartGame } = useGameStart(init , fields, difficult, number, gameStatus);
    
    const { selectField, isFail, isWin } = useGameProcess(fields, gameStatus, difficult , start);

    

    return {
      number,
      difficult,
      fields,
      init,
      start,
      gameStatus,
      canStartGame,
      selectField,
      isFail,
      isWin
    }
  },
  
}
</script>

<style scoped>
  .board-wrapper {
    margin-bottom: 100px;
  }
  
  .board {
    width: 300px;
    background: #eee;
    margin: 0 auto;
  }
  
  .btn {
    background: #42b983cc;
    color: white;
    border: none;
    border-radius: 2px;
    padding: 10px 30px;
    margin: 10px 0;
    cursor: pointer;
    outline: none;
  }
  
  button:hover {
    background: #42b983;
  }

  bottom:disabled {
    opacity: .5%;
  }

  .win {
    color: #42b983;
  }

  .fail {
    color: rgba(255, 0, 0, 0.603);;
  }
</style>