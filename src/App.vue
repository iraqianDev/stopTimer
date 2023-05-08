<template>
  <div>
    <h1>Reaction Timer</h1>
    <button
      class="play"
      :style="{ backgroundColor: !start ? `#42b883` : `#296f4f` }"
      @click="!start && !end ? Begin() : !start && end ? restart() : ''">
      {{ (!start || start) && !end ? "Play" : !start && end ? "Restart" : "" }}
    </button>
  </div>
  <div v-show="show">
    <button class="click" @click="Clicked" v-if="start">Click Me</button>
    <h3 class="result" v-if="!start && time > 0">
      You took {{ time }}ms you {{ speed() }}
    </h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      start: false,
      randomTime: 0,
      show: false,
      time: 0,
      end: false,
    };
  },
  methods: {
    speed() {
      return this.time < 50
        ? "speedy boy"
        : this.time > 50 && this.time < 100
        ? "average human"
        : "grandma";
    },
    Begin() {
      this.start = !this.start;
      this.randomTime = Math.floor(Math.random() * 7);
      if (this.randomTime > 0) {
        setTimeout(() => {
          this.show = !this.show;
          let intervert = setInterval(() => {
            this.time++;
            if (this.start == false) {
              clearInterval(intervert);
              this.time = this.time - 1;
            }
          }, 1);
        }, this.randomTime * 1000);
      }
    },
    Clicked() {
      this.start = false;
      this.end = true;
    },
    restart() {
      this.time = 0;
      this.randomTime = 0;
      this.start = false;
      this.show = false;
      this.end = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.play {
  padding: 15px 25px;
  border: 0;
  border-radius: 10px;
  outline: 0;
  cursor: pointer;
  font-size: 1.5rem;
  color: white;
  transition-duration: 300ms;
}
.click {
  margin-top: 30px;
  padding: 80px 0;
  border: 0;
  border-radius: 10px;
  outline: 0;
  background: #42b883;
  width: 300px;
  max-width: 100%;
  cursor: pointer;
  font-size: 1.5rem;
  color: white;
  transition-duration: 300ms;
}
.result {
  margin-top: 100px;
  font-size: 30px;
}
</style>
