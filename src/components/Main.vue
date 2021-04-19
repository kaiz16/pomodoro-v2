<template>
  <div class="main">
    <p>{{ currentMode }}</p>
    <p>{{ minutes }}:{{ seconds }}</p>

    <div class="buttons">
      <button
        v-on:click="startOrPauseTimer"
        class="mdi mdi-24px"
        v-bind:class="paused ? ' mdi-play-circle-outline' : 'mdi-pause'"
      ></button>

      <button v-on:click="restart" class="mdi mdi-refresh mdi-24px"></button>
    </div>

    <div class="work-setting">
      <p>Work time</p>
      <p>{{ parseInt(workTime / 60, 10) }}</p>
      <button
        v-bind:disabled="paused === false"
        v-on:click="workTime -= 1 * 60"
        class="mdi mdi-minus mdi-24px"
      ></button>
      <button
        v-bind:disabled="paused === false"
        v-on:click="workTime += 1 * 60"
        class="mdi mdi-plus mdi-24px"
      ></button>
    </div>

    <div class="break-setting">
      <p>Break time</p>
      <p>{{ parseInt(breakTime / 60, 10) }}</p>
      <button
        v-bind:disabled="paused === false"
        v-on:click="breakTime -= 1 * 60"
        class="mdi mdi-minus mdi-24px"
      ></button>
      <button
        v-bind:disabled="paused === false"
        v-on:click="breakTime += 1 * 60"
        class="mdi mdi-plus mdi-24px"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      workTime: 60,
      breakTime: 60,
      timer: 120,
      paused: true,
      countdown: null,
    };
  },
  computed: {
    currentMode() {
      return this.timer <= this.breakTime ? "Break" : "Work";
    },
    minutes() {
      let min = parseInt(this.timer / 60, 10);
      if (min < 10) {
        return "0" + min;
      }
      return min;
    },
    seconds() {
      let sec = parseInt(this.timer % 60, 10);
      if (sec < 10) {
        return "0" + sec;
      }
      return sec;
    },
  },
  watch: {
    workTime: function() {
      this.timer = this.workTime + this.breakTime;
    },
    breakTime: function() {
      this.timer = this.workTime + this.breakTime;
    },
    timer: function() {
      if (this.timer < 0) {
        this.restart();
        this.startOrPauseTimer();
        this.$emit("incrementCycle");
      }
    },
  },
  methods: {
    startOrPauseTimer() {
      this.paused = !this.paused;
      this.stop();
      if (!this.timer) {
        return;
      }
      // start the timer
      if (this.paused === false) {
        this.countdown = setInterval(() => {
          this.timer--;
        }, 1000);
      }
    },
    stop() {
      clearInterval(this.countdown);
    },
    restart() {
      this.paused = true;
      this.stop();
      this.timer = this.workTime + this.breakTime;
    },
  },
};
</script>

<style>
.main {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  border: 1px solid #b10046;
  border-radius: 20px;
  width: 20%;
  color: #fff;
  padding: 10px;
}

.buttons {
  display: flex;
  justify-content: center;
  flex-direction: row;
}

.buttons button {
  border: none;
  background: transparent;
  color: white;
  cursor: pointer;
  outline: none;
}
</style>
