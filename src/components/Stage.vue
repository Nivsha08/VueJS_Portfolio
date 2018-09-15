<template>
  <div class="stage lockScroll">
    <transition name="fadeIn">
      <n-portfolio v-if="activeStage === 1"></n-portfolio>
      <n-about v-else-if="activeStage === 2"></n-about>
    </transition>
    <n-loader v-if="activeStage === 3"></n-loader>

  </div>
</template>

<script>
/* eslint-disable */
  import Portfolio from './Portfolio.vue';
  import About from './About.vue';
  import Loader from './Loader.vue';
  import EventBus from '../js/eventBus';

  export default {
    computed: {
      activeStage: function() {
        return this.active;
      }
    },
    components: {
      'n-portfolio': Portfolio,
      'n-about': About,
      'n-loader': Loader
    },
    props: {
      active: {
        type: Number,
        default: 1
      }
    }
  }
</script>

<style scoped>
  .stage {
    margin-top: 120px;
  }

  @media screen and (max-width: 850px) {
    .stage {
      margin-top: 155px;
    }
  }
</style>
