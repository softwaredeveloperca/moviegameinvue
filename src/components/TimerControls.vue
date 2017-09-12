<template>
  <div style="100px;">
    <q-btn class="push" @click="timerControl('play')">
     <i>{{ playing?'ic_play_arrow':'ic_pause'}}</i>
    </q-btn>

    <q-btn @click="timerControl('slower')">
     <i>ic_fast_rewind</i>
    </q-btn>

    <q-btn @click="timerControl('faster')">
     <i>ic_fast_forward</i>
    </q-btn>

    <q-btn @click="timerControl('restart')">
      <i>ic_replay</i>
    </q-btn>
    </div>
</template>

<script>
export default {
  props: {
    isPlaying: Boolean
  },
  data () {
    return {
      playing: this.isPlaying
    }
  },
  methods: {
    timerControl: function (data) {
      this.$emit('timercontrol', data)
    }
  }
}
</script>

<style>
</style>
