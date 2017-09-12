<template>
  <div>

  <div class="row justify-between">
			<div>
	        	<button class="item-value">
			          <i>keyboard_arrow_left</i> Yesterday 
			        </button>
	        </div>

	        <div>
	        <button class="red"> Auto Schedule </button>
	        </div>
	  
	        <div>
	                <button class="item-value">
			          Tomorrow <i>keyboard_arrow_right</i>
			        </button>
	        </div>
</div>


 


  <h4 style="text-align:center">Schedule</h4>

<!--
<ScheduledSlot v-for="slot in slots"
			   v-bind:key="slot.key"
			   :name="slot.key" :time="slot.time">
			   		<div class="row justify-between">
					  <div>{{slot.time}}/div>
					  <div v-on:click="selectMovie">{{slot.key}}</div>
					        <div style="width: 90%; text-align:center" v-if="!terms[slot.key]">
								<q-select style="width: 100%"
					              type="list"
					              v-model="terms[slot.key]"
					              :options="movies"
					              placeholder="Click here to select movie/show"
					            ></q-select>
					  </div>
					  <div>
					  <label>  
					   <button v-if="terms[slot.key]" v-on:click="clearMovie(slot.key)" class="primary small circular">
					  Edit
					</button>


					</label>
					  </div>
					  </div>
					  </div>

			   </ScheduledSlot>-->

  
<div class="row justify-between">
  <div>8:00</div>
  <div v-on:click="selectMovie">{{terms['slot_1']}}</div>
        <div style="width: 90%; text-align:center" v-if="!terms['slot_1']">
			<q-select style="width: 100%"
              type="list"
              v-model="terms['slot_1']"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
  <label>  
   <button v-if="terms['slot_1']" v-on:click="clearMovie('slot_1')" class="primary small circular">
  Edit
</button>


</label>
  </div>
</div>
<br>
<div class="row justify-between">
  <div>8:30</div>
  <div @click="selectMovie">{{terms['slot_2']}}</div>
        <div style="width: 90%; text-align:center;" v-if="!terms['slot_2']">
	<q-select style="width: 100%"
              type="list"
              v-model="terms['slot_2']"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
 <button v-if="terms['slot_2']" v-on:click="clearMovie('slot_2')" class="primary small circular">
  Edit
</button>
  </div>
</div>

 <br>

<div class="row justify-between">
  <div>9:00</div>
  <div @click="selectMovie">{{terms3}}</div>
        <div style="width: 90%; text-align:center" v-if="selectedMovie || !terms3">
	<q-select style="width: 100%"
              type="list"
              v-model="terms3"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
<button v-if="terms3" class="primary small circular">
  Edit
</button>
  </div>
</div>
<br>
<div class="row justify-between">
  <div>10:00</div>
  <div @click="selectMovie">{{terms4}}</div>
        <div style="width: 90%; text-align:center" v-if="selectedMovie || !terms4">
	<q-select style="width: 100%"
              type="list"
              v-model="terms4"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
 <button v-if="terms4" class="primary small circular">
  Edit
</button>
  </div>
</div>

<br>
<div class="row justify-between">
  <div>10:30</div>
  <div @click="selectMovie">{{terms5}}</div>
        <div style="width: 90%; text-align:center" v-if="selectedMovie || !terms5">
	<q-select style="width: 100%"
              type="list"
              v-model="terms5"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
<button v-if="terms5" class="primary small circular">
  Edit
</button>
  </div>
</div>

<br>

<div class="row justify-between">
  <div>11:00</div>
  <div @click="selectMovie">{{terms6}}</div>
        <div style="width: 90%; text-align:center" v-if="selectedMovie || !terms6">
	<q-select style="width: 100%"
              type="list"
              v-model="terms6"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
<button v-if="terms6" @click="clearMovie(6)" class="primary small circular">
  Edit
</button>
  </div>
</div>


  
 </div>
</template>

<script>
import draggable from 'vuedraggable'
import {Toast, Utils} from 'quasar'
import ScheduleSlot from './ScheduleSlot.vue'

const icons = ['alarm', 'email', 'search', 'build', 'card_giftcard', 'perm_identity', 'receipt', 'schedule', 'speaker_phone', 'archive', 'weekend', 'battery_charging_full']
const movies = ['movie 1', 'movie 2', 'movie 3', 'movie 4', 'movie 5', 'movie 6']

function getRandomIcon () {
  return icons[Math.floor(Math.random() * icons.length)]
}
function getRandomStamp () {
  if (Math.floor(Math.random() * 50) % 3 === 0) {
    return `${Math.floor(Math.random() * 10)} min`
  }
}
function getRandomSecondLabel () {
  if (Math.floor(Math.random() * 50) % 4 === 0) {
    return `UID: ${Utils.uid().substring(0, 8)}`
  }
}
function parseMovies () {
  return movies.map(movie => {
    return {
      label: movie,
      secondLabel: getRandomSecondLabel(),
      icon: getRandomIcon(),
      stamp: getRandomStamp(),
      value: movie
    }
  })
}
export default {
  data () {
    return {
      terms: [],
      terms2: '',
      terms3: '',
      terms4: '',
      terms5: '',
      terms6: '',
      selectedMovie: '',
      movies: parseMovies(),
      select: 'fb',
      cat1: '',
      slots: [
        {
          name: 'Slot 1',
          key: 'Slot_1',
          time: '8:00'
        },
        {
          name: 'Slot 2',
          key: 'Slot_2',
          time: '8:30'
        },
        {
          name: 'Slot 3',
          key: 'Slot_3',
          time: '9:00'
        },
        {
          name: 'Slot 4',
          key: 'Slot_4',
          time: '9:30'
        },
        {
          name: 'Slot 5',
          key: 'Slot_5',
          time: '10:00'
        },
        {
          name: 'Slot 6',
          key: 'Slot_6',
          time: '10:30'
        },
        {
          name: 'Slot 7',
          key: 'Slot_7',
          time: '11:00'
        },
        {
          name: 'Slot 8',
          key: 'Slot_8',
          time: '11:30'
        }
      ],
      multipleSelect: ['goog', 'twtr'],
      selectOptions: [
        {
          label: 'Google',
          value: 'goog'
        },
        {
          label: 'Facebook',
          value: 'fb'
        },
        {
          label: 'Twitter',
          value: 'twtr'
        },
        {
          label: 'Apple Inc.',
          value: 'appl'
        },
        {
          label: 'Oracle',
          value: 'ora'
        }
      ]
    }
  },
  methods: {
    selectMovie () {
      this.selectedMovie = 1
    },
    clearMovie (slotname) {
      this.terms[slotname] = ''
      return true
    },
    search (terms, done) {
      setTimeout(() => {
        done(Utils.filter(terms, {field: 'value', list: parseMovies()}))
      }, 500)
    },
    selected (item) {
      Toast.create(`Selected suggestion "${item.label}"`)
    },
    checkall () {
      alert('dfdfd')
    },
    components: {
      draggable,
      ScheduleSlot
    }
  }
}
</script>

<style>
.small {
	font-size: 0.55rem;
}
</style>
