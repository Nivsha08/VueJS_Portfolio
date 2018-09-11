<template>
  <transition name="fadeIn">
  <div class="fullDisplay" v-if="showFullDisplay" :class="{lockScroll: showFullDisplay}">
    <div class="displayNav">
      <p class="like"><span @click="like(item.i)" class="fa-heart" :class="{far: !item.isLiked, fas: item.isLiked, red: item.isLiked}"></span>
        {{ item.likes }}</p>
      <div class="navButtons">
        <span @click="prevItem()" class="fas fa-chevron-left"></span>
        <span @click="nextItem()" class="fas fa-chevron-right"></span>
        <span @click="closeFullDisplay" class="fas fa-times"></span>
      </div>
    </div>
    <h2>{{item.title}}</h2>
    <img :src="item.src">
  </div>
  </transition>
</template>

<script>
  import EventBus from '../js/eventBus.js';

  export default {
    data() {
      return {
        showFullDisplay: false,
        item: this.findItem(this.itemId)
      }
    },
    props: {
      images: Array,
      itemId: Number
    },
    methods: {
      findItem(id) {
        let a = this.images;
        return a.find(function(e){
          return id === e.i;
        });
      },
      like(id) {
        EventBus.$emit('like', id);
      },
      openFullDisplay(id) {
        this.showFullDisplay = true;
        this.item = this.findItem(id);
        document.body.classList.add("overflowHidden");
      },
      nextItem() {
        if (this.item.i + 1 < this.images.length) {
          this.openFullDisplay(this.item.i + 1);
        }
      },
      prevItem() {
        if (this.item.i - 1 >= 0) {
          this.openFullDisplay(this.item.i - 1);
        }
      },
      closeFullDisplay() {
        this.showFullDisplay = !this.showFullDisplay;
        document.body.classList.remove("overflowHidden");
      }
    },
    mounted() {
      EventBus.$on('openFullDisplay', function(data) {
        this.openFullDisplay(data);
      }.bind(this));
    }
  }
</script>

<style src="../css/FullDisplay.css">
</style>
