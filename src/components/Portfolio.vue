<template>
  <div class="portfolio">
    <n-fullDisplay :itemId="fullDisplayItem" :images="images"></n-fullDisplay>
    <div class="container">
      <n-item v-for="p in images" :image="p" :key="p.i"></n-item>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
  import Item from './Item.vue';
  import FullDisplay from './FullDisplay.vue';
  import EventBus from '../js/eventBus.js';

export default {
    data() {
      return {
        fullDisplayItem: 0,
        images: []
      }
    },
    components: {
      'n-item': Item,
      'n-fullDisplay': FullDisplay
    },
    methods: {
      like(i) {
        let v = this.images.find(function(e) {
            return e.i === i;
        });
        if (!v.isLiked) {
          v.likes++;
          v.isLiked = !v.isLiked;
        }
        else {
          v.likes--;
          v.isLiked = !v.isLiked;
        }
        this.updateImages();
      },
      fetchImages() {
        console.log("here");
        this.$http.get('https://nivsha-portfolio.firebaseio.com/images.json')
          .then(response => response.json())
          .then(data => {
            this.images = data;
          });
      },
      updateImages() {
        this.$http.put('https://nivsha-portfolio.firebaseio.com/images.json', this.images);
      }
    },
    mounted() {
      this.fetchImages();
      EventBus.$on('like', function(data) {
        this.like(data);
      }.bind(this));
      EventBus.$on('openFullDisplay', function(data) {
        this.fullDisplayItem = data;
      }.bind(this));
    }
  }
</script>

<style src="../css/Portfolio.css"></style>
