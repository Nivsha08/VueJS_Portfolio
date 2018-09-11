<template>
  <div class="loader">
    <span class="fas fa-circle-notch fa-3x"></span>
  </div>
</template>

<script></script>

<style scoped>
  .loader {
    width: 100%;
    height: 400px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
  
  .loader span {
    color: #ccc;
    transform-origin: center;
    transform: rotate(40deg);
    animation: circular 1.2s 0s ease-in-out infinite;
  }

  @keyframes circular {
    80% {
      transform: rotate(-320deg);
    }
    100% {
      transform: rotate(-320deg);
    }
  }
</style>
