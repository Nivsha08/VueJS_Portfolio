<template>
  <div class="navbar">
    <div class="container">
      <a @click="changeView(1)" class="brand">NIVSHA</a>
      <ul>
        <li @click="changeView(1)"><a :class="{active: activeLink === 1}">Portfolio</a></li>
        <li @click="changeView(2)"><a :class="{active: activeLink === 2}">About</a></li>
        <li><a href="https://www.facebook.com/nivsha">Facebook</a></li>
        <li><a href="https://www.github.com/nivsha08">Github</a></li>
        <li><a href="https://www.instagram.com/nivsha_graphics">Instagram</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
  import EventBus from '../js/eventBus.js';

  export default {
    computed: {
      activeLink: function(){
        return this.active;
      }
    },
    props: {
      active: {
        type: Number,
        default: 1
      }
    },
    methods: {
      changeView(n) {
        EventBus.$emit('stageChange', n);
      }
    }
  }
</script>

<style src="../css/Navbar.css">
</style>
