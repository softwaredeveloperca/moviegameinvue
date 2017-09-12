<template>
  <q-layout>
    <div slot="header" class="toolbar">
    
    <q-toolbar-title :padding="2" class="text-center">
      Movie Game
    </q-toolbar-title>

    <button>
      <i>timer</i>
    </button>
    <button>
      <i>tv</i>
    </button>
    <button v-if="loggedIn" @click="logoff">
      <i>usb</i>
    </button>
  </div>

    <q-tabs slot="navigation" class="blue justified" :refs="$refs"
  default-tab="tab-1" @change="setRoomTitle(refs)">
    
    <q-tab
      icon="tv"
      name="tab-1"
       
     
    >
      {{mainTabText}}

    </q-tab>
    <q-tab  
      icon="today"
      name="tab-2"
      align="left"
      @click="setRoomTitle('TODAY')"
    >
      Schedule
    </q-tab>
    
    <q-tab
      icon="movie"
      components="movie"
      name="tab-3"
      
    >
      Movies
    </q-tab>
    <q-tab
      icon="store"
      name="tab-4"
      
    >
      Ads
    </q-tab>
    <q-tab
      icon="people"
      name="tab-5"
      
    >
      Audience
    </q-tab>

   
  </q-tabs>


  <div class="card">
  <div display="flex" style="display: flex" class="card-title bg-warning text-white">
    <div style="flex: 1 1 auto;" v-if="currentSchedule" v-for="schedule in currentSchedule">
      <div v-if="schedule[0]">
      <h4>{{schedule[0]['MovieName']}} <small class="bg-secondary label text-white small">Part: {{schedule[0]['MoviePart']}}</small></h4>
      {{schedule[0]['PlayerName']}}<br>
      {{schedule[0]['MovieType']}}
      </div>
    </div>
  </div>
  <div class="card-content card-force-top-padding">
    <div ref="tab-1">
    <div v-if="!loggedIn">Name: <input type="name" v-model="loginName" placeholder="Unknown" />
    <input type="button" @click="login" value="Join" />
    </div>

    <WhatsOn v-if="loggedIn"></WhatsOn>
    </div>
  <div ref="tab-2"><Schedule v-if="loggedIn" /></div>
  <div ref="tab-3">
    <Movies  
      v-on:getMyMovies="getMyMovies"
      v-on:buyMovie="buyMovie"
      v-on:sellMovie="sellMovie"  
      v-on:getAvailableMovies="getAvailableMovies" 
      v-bind:movies="movies" 
      v-if="loggedIn" />
  </div>
  <div ref="tab-4"><Ads  v-if="loggedIn" /></div>
  <div ref="tab-5"><Audience v-if="loggedIn" /></div>
  </div>
</div>   



<div slot="footer" class="toolbar"> 
  <q-toolbar-title :padding="2" class="text-left">
      <GroupTime v-if="loggedIn" v-bind:time-counter="counter" v-bind:time-day="day" />
    </q-toolbar-title>



    <TimerControls v-on:timercontrol="timerControl" v-bind:isPlaying="playing" v-if="loggedIn" />

  </div> 
  
  </q-layout>
</template>

<script>
import GroupTv from './GroupTv.vue'
import GroupTime from './GroupTime.vue'
import TimerControls from './TimerControls.vue'
import Movies from './Movies.vue'
import Ads from './Ads.vue'
import WhatsOn from './WhatsOn.vue'
import Schedule from './Schedule.vue'
import Chat from './Chat.vue'
import Audience from './Audience.vue'

export default {

  data () {
    return {
      items: [],
      loginName: '',
      mainTabText: 'Join',
      loggedIn: false,
      counter: 0,
      day: 1,
      playing: true,
      movies: [],
      ads: [],
      currentSchedule: []
    }
  },
  components: {
    GroupTv,
    GroupTime,
    TimerControls,
    Movies,
    Ads,
    Schedule,
    WhatsOn,
    Chat,
    Audience
  },
  props: {
    socket: {
      default: null
    },
    roomTitle: {
      default: 'WhatsOn'
    }
  },
  methods: {
    login () {
      if (!this.loginName) {
        this.loginame = 'Unknown Player'
      }
      this.$socket.emit('login', this.loginName)
      this.getMovies()
    },
    logoff () {
      this.loggedIn = false
      this.mainTabText = 'Join'
      this.$socket.emit('logout', this.loginName)
    },
    getMovies () {
      this.$socket.emit('getMovies', 'My')
    },
    getMyMovies: function (data) {
      this.$socket.emit('getMovies', 'My')
      this.buyMovie()
    },
    buyMovie: function (data) {
      this.$socket.emit('buyMovie', data)
    },
    timerControl: function (data) {
      console.log(data)
      this.$socket.emit('timercontrol', data)
    },
    sellMovie: function (data) {
      this.$socket.emit('sellMovie', data)
    },
    getAvailableMovies: function (data) {
      this.$socket.emit('getMovies', 'All')
    },
    getSchedule: function (data) {
      this.$socket.emit('getSchedule', 'Today')
    },
    setRoomTitle (title) {
      this.roomTitle = title
    }
  },
  sockets: {
    connect: function () {
      console.log('socket connected')
    },
    customEmit: function (val) {
      console.log('this method was fired by the socket server. eg: io.emit("customEmit", data)')
    },
    newgame: function (data) {
      console.log('new game')
      this.loggedIn = true
      this.mainTabText = 'What\'s On'
    },
    movies: function (data) {
      this.movies = data
    },
    scheduledata: function (data) {
      console.log(data)
      let adata = data
      this.currentSchedule = adata
    },
    tick: function (data) {
      console.log(data)
      if (data) {
        this.day = data.shift()
        console.log(this.day)
        if (data === this.counter) {
          this.playing = false
        }
        else {
          this.counter = data
          this.playing = true
        }
      }
    }
  }
}
</script>

<style lang="stylus">
.logo-container
  width 192px
  height 268px
  perspective 800px
  position absolute
  top 50%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d
</style>
