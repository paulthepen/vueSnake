<template>
  <div class="score">Apples Eaten: {{applesEaten}}</div>
  <div class="board" :style="boardStyle">
    <snakeElement :state="snakeState" />
    <appleElement :pos="applePos" />
  </div>
</template>

<script>
import snakeElement from './SnakeElement.vue';
import appleElement from './AppleElement.vue';

 const generateRandomCoordinates = () => {
      const x = Math.floor(Math.random()*400/10)*10;
      const y = Math.floor(Math.random()*400/10)*10;
       return [x, y];
    }

export default {
  name: 'GameBoard',
  data() {
    return {
      snakeState: [{ key: 2, pos: [190, 200] }, { key: 1, pos: [200, 200] }],
      applePos: [320, 300],
      direction: 'R',
      applesEaten: 0
    }
  },
  props: [],
  components: { snakeElement, appleElement },
  computed: {
    boardStyle() {
      return {
        position: 'absolute',
        width: '400px',
        height: '400px',
        left: "calc(50% - 200px)",
      }
    },
  },
  methods: {
    checkCollisions() {
      const head = this.snakeState[this.snakeState.length-1]
      const headPos = head.pos;
      if (headPos[0] == this.applePos[0] && headPos[1] == this.applePos[1]) {
        this.applePos = generateRandomCoordinates();
        this.snakeState.unshift({key: head.key + 1, pos: this.snakeState[0].pos});
        this.applesEaten++;
      }
      if (headPos.includes(-10) || headPos.includes(400)) {
        alert("Game over!");
        this.snakeState =  [{ key: 2, pos: [190, 200] }, { key: 1, pos: [200, 200] }],
        this.applePos =  [320, 300],
        this.direction = 'R',
        this.applesEaten = 0
      }
      for (let part of this.snakeState) {
        if (this.snakeState.indexOf(part) == this.snakeState.length-1) {
          return;
        }
        if (part.pos[0] == headPos[0] && part.pos[1] == headPos[1]) {
            alert("Game over!");
            this.snakeState =  [{ key: 2, pos: [190, 200] }, { key: 1, pos: [300, 300] }],
            this.applePos =  [320, 300],
            this.direction = 'R',
            this.applesEaten = 0
            return;
        }
      }
    },
    renderSnake() {
      const head = this.snakeState[this.snakeState.length - 1];
      switch (this.direction) {
        case 'R':
          this.snakeState.push({ key: head.key + 1, pos: [head.pos[0] + 10, head.pos[1]] });
          this.snakeState.shift();
          break;
        case 'L':
          this.snakeState.push({ key: head.key + 1, pos: [head.pos[0] - 10, head.pos[1]] });
          this.snakeState.shift();
          break;
        case 'U':
          this.snakeState.push({ key: head.key + 1, pos: [head.pos[0], head.pos[1] - 10] });
          this.snakeState.shift();
          break;
        case 'D':
          this.snakeState.push({ key: head.key + 1, pos: [head.pos[0], head.pos[1] + 10] });
          this.snakeState.shift();
          break;
      }
    },
    changeDirection(val) {
      switch (val.keyCode) {
        case 37: this.direction = 'L'; break;
        case 38: this.direction = 'U'; break;
        case 40: this.direction = 'D'; break;
        case 39: this.direction = 'R'; break;
      }
    }
  },
  mounted() {
    window.addEventListener('keydown', (e) => {
      this.changeDirection(e);
    }),
      setInterval(() => {
        this.renderSnake();
        this.checkCollisions();
      }, 200);
  }
}
</script>

<style scoped>
.board {
  background-color: navy;
}

.score {
  width: 100%;
  color: aqua;
  text-align: right;
}
</style>
