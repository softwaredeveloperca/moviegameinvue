<template>
  <div>{{formatTime()}}   
</div>
</template>

<script>

export default {
  props: {
    timeCounter: Array,
    timeDay: Number
  },
  data () {
    return {
      currentCount: this.timeCounter,
      currentDay: this.timeDay,
      returnstr: ''
    }
  },
  methods: {
    formatTime: function () {
      this.returnstr = (this.timeCounter % 60) < 10 ? ('0' + this.timeCounter % 60) : (this.timeCounter % 60)
      this.returnstr = Math.floor(this.timeCounter / 60) + ' : ' + this.returnstr
      this.returnstr = 'Day ' + this.timeDay + ' ' + this.returnstr
      return this.returnstr
    }
  }
}
</script>

<style>
</style>
