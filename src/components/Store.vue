<template>
  <div :class="{ open: showMenu }">
    <div class="store-toggle toggle" @click="showMenu = !showMenu" title="Open store">
      <eva-icon name="shopping-cart-outline"></eva-icon>
    </div>
    <div class="store" v-if="showMenu">
      <div class="store-inner">
        <h3>Store</h3>
        <div>
          <h4>Gate</h4>
          <p>Gates receive passengers &amp; planes. They require staff.</p>
          <button @click="buyGate" :class="{ disabled: $root.player.gates.length === 16 || $root.player.cash < 50000 || !$root.player.runways.length }"><eva-icon name="upload-outline"></eva-icon> Build gate ($50,000)</button>
        </div>
        <div>
          <h4>Runway</h4>
          <p>Runways allow planes to land and takeoff.</p>
          <button @click="buyRunway" :class="{ disabled: $root.player.runways.length === 5 || $root.player.cash < 250000 }"><eva-icon name="arrowhead-up-outline"></eva-icon> Build runway ($250,000)</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { bus } from '@/main'

export default {
  name: 'store',
  components: {
    bus
  },
  data () {
    return {
      showMenu: false
    }
  },
  created () {
  },
  methods: {
    buyPlane () {
      bus.$emit('buy-plane')
    },
    buySchedule () {
      bus.$emit('buy-schedule')
    },
    buyGate () {
      bus.$emit('buy-gate')
    },
    buyRunway () {
      bus.$emit('buy-runway')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.store {
  position: fixed;
  bottom: 15px;
  right: 90px;
  width: 250px;
  z-index: 30;
}

.store-inner {
  background-color: white;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 5px 10px -3px rgba(0, 0, 0, .5);
}

.store-toggle {
  top: auto;
  bottom: 15px;
}
</style>
