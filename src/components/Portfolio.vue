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
        'images': [
          {
            i: 0,
            src: 'https://images.pexels.com/photos/1078058/pexels-photo-1078058.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Joy",
            description: "Windy and warm",
            likes: 19,
            isLiked: false
          },
          {
            i: 1,
            src: 'https://images.pexels.com/photos/169928/pexels-photo-169928.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Self Shoot",
            description: "The eye of the beholder",
            likes: 22,
            isLiked: true
          },
          {
            i: 2,
            src: 'https://images.pexels.com/photos/1227497/pexels-photo-1227497.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Wall Paintings",
            description: "Freestyle & colorful",
            likes: 4,
            isLiked: false
          },
          {
            i: 3,
            src: 'https://images.pexels.com/photos/1401796/pexels-photo-1401796.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Running",
            description: "Personal challenges motivation",
            likes: 0,
            isLiked: false
          },
          {
            i: 4,
            src: 'https://images.pexels.com/photos/160426/lead-man-sun-sunglasses-160426.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Thoughts",
            description: "Through the sunglasses",
            likes: 3,
            isLiked: false
          },
          {
            i: 5,
            src: 'https://images.pexels.com/photos/226460/pexels-photo-226460.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Foggy Highway",
            description: "Mid-day downtown",
            likes: 12,
            isLiked: true
          },
          {
            i: 6,
            src: 'https://images.pexels.com/photos/698878/pexels-photo-698878.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Baby Steps",
            description: "Mother and son",
            likes: 19,
            isLiked: true
          },
          {
            i: 7,
            src: 'https://images.pexels.com/photos/1211771/pexels-photo-1211771.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Desert Rally",
            description: "Desert car racing rally",
            likes: 20,
            isLiked: false
          },
          {
            i: 8,
            src: 'https://images.pexels.com/photos/1209843/pexels-photo-1209843.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Colorful eyes",
            description: "Portrait",
            likes: 3,
            isLiked: false
          },
          {
            i: 9,
            src: 'https://images.pexels.com/photos/196666/pexels-photo-196666.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            title: "Sunset Together",
            description: "Beautiful sunset",
            likes: 19,
            isLiked: false
          },
        ]
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
      }
    },
    mounted() {
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
