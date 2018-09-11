<template>
  <div id="app">
    <n-nav :active="onStage"></n-nav>
    <n-stage :active="onStage"></n-stage>
    <n-footer v-if="onStage === 1 || onStage === 2"></n-footer>
  </div>
</template>

<script>
/* eslint-disable */
import Navbar from './components/Navbar.vue';
import Stage from './components/Stage.vue';
import Footer from './components/Footer.vue';
import EventBus from './js/eventBus.js';

export default {
  data() {
    return {
      onStage: 1
    }
  },
  components: {
    'n-nav': Navbar,
    'n-stage': Stage,
    'n-footer': Footer
  },
  mounted() {
    EventBus.$on('stageChange', function(data) {
      if (this.onStage === data) {
        return;
      }
      this.onStage = 3; //show loader
      setTimeout(function() {
        this.onStage = data;
      }.bind(this), 1500);
    }.bind(this));
  },
  name: 'App'
}
</script>

<style>
  .fadeIn-enter-active {
    animation: fadeIn .3s;
  }

  .fadeIn-leave-active {
    animation: fadeIn .3s reverse;
  }

  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
