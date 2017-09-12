<template>
  <div><h1>Ads</h1>
  <button class="primary" @click="clickMethod()">
  My Ads
</button>
<button class="primary" @click="clickMethod()">
  Get Ads
</button>
  	<q-slider infinite arrows dots actions class="text-white">
  <div slot="slide" class="bg-primary">
    Slide 1
  </div>
  <div slot="slide" class="bg-secondary">
    Slide 2
  </div>
  <div slot="slide" class="bg-tertiary">
    Slide 3
  </div>
  <i slot="action" @click="someMethod()">
    camera_enhance
  </i>
  <i slot="action" @click="someOtherMethod()">
    bookmark_border
  </i>
  <i slot="action" @click="thirdMethod()">
    add_shopping_cart
  </i>
</q-slider>
  </div>
</template>
  

<script>
export default {
  data () {
    return {}
  }
}
</script>

<style>
</style>
