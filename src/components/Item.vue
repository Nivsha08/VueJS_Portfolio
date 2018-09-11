<template>
  <div class="item">
    <div @click="openItem" class="overlay">
      <h2>{{ itemTitle }}</h2>
      <p>{{ itemDescription }}</p>
      <p class="like"><span @click="like($event, id)" class="fa-heart" :class="{far: !isLiked, fas: isLiked, red: isLiked}"></span> {{ likes }}</p>
    </div>
    <img :src="source" :title="itemTitle">
  </div>
</template>

<script>
/* eslint-disable */
  import EventBus from '../js/eventBus.js';
  export default {
    data() {
      return {
        id: this.image.i,
        source: this.image.src,
        itemTitle: this.image.title,
        itemDescription: this.image.description
      }
    },
    computed: {
      likes: function() {
        return this.image.likes;
      },
      isLiked: function() {
        return this.image.isLiked;
      }
    },
    methods: {
      like($event, i) {
        event.stopPropagation();
        EventBus.$emit('like', i);
      },
      openItem() {
        EventBus.$emit('openFullDisplay', this.id);
      }
    },
    props: {
      image: Object
    }
  }
</script>

<style src="../css/Item.css"></style>
