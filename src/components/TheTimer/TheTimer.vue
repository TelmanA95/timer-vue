<template>
    <div class="timer">
      <div :class="timerActive && !timerPaused ? 'play-timer' : 'time'">
        <p>{{ formatTime }}</p>
      </div>
      <div :class="timerActive && !timerPaused ? 'white' : 'gray'"></div>
      <div class="btns">
        <img :src="timerActive && !timerPaused ? pauseSrc : playSrc" @click="toggleTimer" alt="Play">
        <img :src="timerActive ? stopWhite : stop" @click="stopTimer" v-if="shouldDisplayStopResetButtons" alt="Stop">
        <img :src="shouldDisplayStopResetButtons ? resetWhite : reset" @click="resetTimer" v-if="shouldDisplayStopResetButtons && timerActive" alt="Restore">
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      playSrc:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABEAAAAUCAYAAABroNZJAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAD2SURBVHgBpZTbCYMwFIaTILhGR2hH6QZeUHCK6gb65JPWTeoGukEzgo8KXnoiWlpJNKf9QAyJfv5HTkLuQJqmJ/IHNM/zaR5QGsItsW27IUjYOpimKYSryrLMIkjeSb4mKa3btr0GQcCJBkw2CYnOpmk+df8X21sEmQWyx1GJ0nIU8L7vr77v1wSTZMPJMIxKViJGMrOUKGS3dQ5TjgwO0gidZMs4jvxXSSMSQD9dPM8rDYIEXiygEaPPRsRIymEYIvHl7YKOZI7uum6seuBIkojd7TjO7s5WSZTRdSR8iV4QBKtE1J0wxuKj6CpJ2XWdrXt2yHgBpCqB12pVxYoAAAAASUVORK5CYII=",
      pauseSrc:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAUCAYAAAC07qxWAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAmSURBVHgB7cohEgAACAJB8P9/VoKBaHbYescWLAqMt8JRxoy/xwFUNQgkB213dQAAAABJRU5ErkJggg==",
      stopWhite:'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAlSURBVHgB7cxBDQAACAOxgX/PMBH7LLkK6JwpaBVGSEhISNgSPrMVBCQ1YTjHAAAAAElFTkSuQmCC',
      stop:'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAnSURBVHgB7cxBDQAACAOxgX8Nswom9llyFdCxfQpahRESEhIStoQPg3YDAf73BxwAAAAASUVORK5CYII=',
      reset:'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAyElEQVR4nO1VOwoCMRTcRr2C4EmEPY+1t9A2nYHMS9Aux7DQiyiewcrlyQbcn8nbtBkYCPlNJuRNqqogBwD2RPRJ5BPA0Xu//LfhjtnrOwtEmIfRzY0xWwBvJrdnuK2Dk8GgtXYN4BFOAeDlnNtIRcL6TqfWegHg2rcK4K6UWmULEJGeuk8ALltANCGCIhBFuaJRRJ75KfuZ6olCJaLboFDn1oFNjRoOqnZCLRUxKWHJUSuM5kss7jvgz6IV+TpJIX9KUrcF1S8aXciY8hXotF4AAAAASUVORK5CYII=',
      resetWhite:'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAq0lEQVR4nO2UvQ3CMBCF3ZCsgMQkljJP6mwRRoAOJZtQwCKgzED1ISNHihwn5x9Kf9I1tnXPz/I9pQo5AB3hvIEzUO01bE05awNx9FvNNfCxpRPcNrMT3+YReC1uMQGnBJEf7uIBuHusPoH6HwLXnfe8ZQtEHRAoAiLlibwI3/yS/U3ZHtTHalBT54DQqLGRa2gSRLQYliZqiWOU4t4VqKzI7CSELtZtQS35Ao2HRjghsRAxAAAAAElFTkSuQmCC',
      hours: 0,
      minutes: 0,
      seconds: 0,
      timerActive: false,
      timerPaused: false,
      intervalId: null,
    };
  },
  methods: {
    toggleTimer() {
      this.timerPaused = this.timerActive && !this.timerPaused;
      this.timerActive = !this.timerActive;
      this.timerPaused ? clearInterval(this.intervalId) : (this.intervalId = setInterval(() => this.updateTime(), 1000));
    },
    updateTime() {
      this.seconds++;
      if (this.seconds === 60) {
        this.seconds = 0;
        this.minutes++;
        if (this.minutes === 60) {
          this.minutes = 0;
          this.hours++;
        }
      }
    },
    resetTimer() {
      this.seconds = 0;
      this.minutes = 0;
      this.hours = 0;
      this.timerActive = false;
      this.timerPaused = false;
      clearInterval(this.intervalId);
    },
    stopTimer() {
      this.resetTimer();
    },
    addTimer() {
      const newTimer = {
        hours: 0,
        minutes: 0,
        seconds: 0,
        timerActive: false,
        timerPaused: false,
        intervalId: null,
      };
      this.timers.push(newTimer);
    },
  },
  computed: {
    formatTime() {
      return `${this.hours.toString().padStart(2, '0')}:${this.minutes.toString().padStart(2, '0')}:${this.seconds.toString().padStart(2, '0')}`;
    },
    shouldDisplayStopResetButtons() {
      return this.timerActive || this.seconds > 0 || this.minutes > 0 || this.hours > 0;
    },
  },
};
</script>

<style scoped>

.container{
  margin: 10px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.timer{
  width: 100%;
  max-width: 225px;
  height: 120px;
  background: #696969;
  margin: 23px 25px;
}
.btns{
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 10px;
}

img{
  margin: 0 10px;
  cursor: pointer;
}

.time{
  display: flex;
  justify-content: center;
  font-family: 'Gotham';
  font-size: 22px;
  color: #9E9E9E;
}

img{
  width: 20px;
  height: 20px;
}

.play-timer{
  display: flex;
  justify-content: center;
  font-family: 'Gotham';
  font-size: 22px;
  color: #fff;
}
.white{
  width: 100%;
  height: 2px;
  background: #fff;
  margin: 0 0 10px 0;
}
.gray{
  width: 100%;
  height: 2px;
  background: #9E9E9E;
  margin: 0 0 10px 0;
}
</style> 