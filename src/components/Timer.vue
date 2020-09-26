<template>
  <div class="timer">
    <input
      class="timer__input"
      type="text"
      v-model="time"
      v-on:keyup="replaceUnits"
    />
    <button class="timer__start-btn" @click="startTimer">Start</button>
  </div>
</template>

<script>
export default {
  name: "Timer",
  data() {
    return {
      isRunning: false,
      time: "",
      timer: null,
      timeUnits: [],
    };
  },
  methods: {
    startTimer() {
      this.isRunning = true;
      this.timeUnits = this.time.split(":");
      let seconds, minutes, hours;
      if (this.timeUnits.length === 1) {
        seconds = Number(this.timeUnits[0]);
      }
      if (this.timeUnits.length === 2) {
        minutes = Number(this.timeUnits[0]);
        seconds = minutes * 60 + Number(this.timeUnits[1]);
      }
      if (this.timeUnits.length === 3) {
        minutes = Number(this.timeUnits[1]);
        hours = Number(this.timeUnits[0]);
        seconds = hours * 3600 + minutes * 60 + Number(this.timeUnits[2]);
      }
      this.timer = setInterval(() => {
        seconds ? "" : this.stop();
        this.time = this.timeFormat(seconds);
        seconds--;
      }, 1000);
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.timer);
      this.timer = null;
    },
    reset() {
      this.stop();
      this.time = 0;
      this.secondes = 0;
      this.minutes = 0;
    },
    setTime(payload) {
      this.time = payload.minutes * 60 + payload.secondes;
    },
    replaceUnits() {
      this.timeUnits = this.time.split(":");
      let regex = /[0-9]|:/;
      let timeArr = this.time.split("");
      for (let i = 0; i < this.time.length; i++) {
        if (!regex.test(this.time[i])) {
          timeArr[i] = "";
          this.time = timeArr.join("");
        }
      }
      if (this.timeUnits.length === 2) {
        if (this.timeUnits[1] > 59) {
          this.timeUnits[1] = "59";
          this.time = this.timeUnits[0] + ":" + this.timeUnits[1];
        }
      }
      if (this.timeUnits.length === 3) {
        if (this.timeUnits[1] > 59) {
          this.timeUnits[1] = "59";
          this.time =
            this.timeUnits[0] +
            ":" +
            this.timeUnits[1] +
            ":" +
            this.timeUnits[2];
        }
        if (this.timeUnits[2] > 59) {
          this.timeUnits[2] = "59";
          this.time =
            this.timeUnits[0] +
            ":" +
            this.timeUnits[1] +
            ":" +
            this.timeUnits[2];
        }
      }
    },
    timeFormat(sec) {
      let hours = sec / 3600,
        minutes = (sec / 60) % 60,
        seconds = sec % 60;
      if (Math.floor(hours)) {
        return (
          this.toNum(hours) +
          ":" +
          this.toNum(minutes) +
          ":" +
          this.toNum(seconds)
        );
      } else if (Math.floor(minutes)) {
        return this.toNum(minutes) + ":" + this.toNum(seconds);
      } else {
        return this.toNum(seconds);
      }
    },
    toNum(val) {
      val = Math.floor(val);
      return val < 10 ? "0" + val : val;
    },
  },
};
</script>
