<template>
  <div class="row justify-between">AAAA
  <div>8:00</div>
  <div>{{slot_key}}</div>
        <div style="width: 90%; text-align:center" v-if="!slot_key">
			<q-select style="width: 100%"
              type="list"
              v-model="this.slot_key"
              :options="movies"
              placeholder="Click here to select movie/show"
            ></q-select>
  </div>
  <div>
  <label>  
   <button v-if="slot_key" v-on:click="clearMovie(slot_key)" class="primary small circular">
  		Edit
	</button>
</label>
  </div>
  </div>
</template>

<script>
export default {
  props: ['name', 'time'],
  data () {
    return {
      'slot_key': this.name,
      'slot_time': this.time
    }
  }
}
</script>

<style>
</style>
