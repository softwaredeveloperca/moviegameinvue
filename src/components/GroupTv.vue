<template>
  <div>a{{nowPlaying()}}</div>
</template>

<script>
export default {
  props: {
    whatson: Object
  },
  data () {
    return {
      currentWhatsOn: this.whatson,
      returnStr: ''
    }
  },
  methods: {
    nowPlaying: function () {
      this.returnStr = 'baaa' + this.whatson[0]
      return this.returnStr
      // for (var x = 0; x < this.currentWhatsOn.length; x++) {
      //  if (this.currentWhatsOn[x].MovieName.length > 0) {
          // this.returnStr = this.returnStr + this.currentWhatsOn[0][x].PlayerName + ' ' + this.currentWhatsOn[0][x].MovieName + ' Part ' + this.currentWhatsOn[0][x].MoviePart
      //  }
      // }
      // return this.returnStr
    }
  }
}
</script>

<style>
</style>
