<template>
    <div class="slideshow-container">
      <div class="image-container">
        <img :src="currentImage" :alt="currentCaption" class="slideshow-image">
      </div>
      <br>
      <div class="controls">
        <button @click="toggleSlideshow" class="slideshow-button">{{ slideshowActive ? 'Stop' : 'Start' }}</button>
        <button @click="showPrevImage" class="prev-button">Prev</button>
        <button @click="showNextImage" class="next-button">Next</button>
      </div>
      <p class="caption">{{ currentCaption }}</p>
      <p class="index">{{ currentIndex + 1 }} / {{ images.length }}</p>
    </div>
  </template>
  
  <script>
  const images = [
    {
      src: 'https://i.pinimg.com/564x/b2/11/c1/b211c1336bee3015d725d94e07a4b4ee.jpg',
      caption: 'Duck Cute',
    },
    {
      src: 'https://i.pinimg.com/564x/2d/cc/41/2dcc41573569063ad05cf4db3511fb9a.jpg',
      caption: 'Beautiful girl',
    },
  ];
  
  export default {
    data() {
      return {
        currentIndex: 0,
        slideshowActive: false,
        intervalId: null,
      };
    },
    computed: {
      currentImage() {
        return images[this.currentIndex].src;
      },
      currentCaption() {
        return images[this.currentIndex].caption;
      }
    },
    methods: {
      showNextImage() {
        this.currentIndex = (this.currentIndex + 1) % images.length;
      },
      showPrevImage() {
        this.currentIndex = (this.currentIndex - 1 + images.length) % images.length;
      },
      toggleSlideshow() {
        if (this.slideshowActive) {
          this.stopSlideshow();
        } else {
          this.startSlideshow();
        }
      },
      startSlideshow() {
        this.slideshowActive = true;
        this.intervalId = setInterval(() => {
          this.showNextImage();
        }, 3000);
      },
      stopSlideshow() {
        this.slideshowActive = false;
        clearInterval(this.intervalId);
      }
    },
    beforeDestroy() {
      clearInterval(this.intervalId);
    }
  };
  </script>
  
  <style scoped>
  .slideshow-container {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    max-width: 400px;
    max-height: 300px;
  }
  
  .image-container {
    max-width: 100%;
    max-height: 100%;
    overflow: hidden;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .slideshow-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 8px;
    animation: fadeInOut 1.5s ease-in-out;
  }
  
  .next-button,
  .prev-button,
  .slideshow-button {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .next-button:hover,
  .prev-button:hover,
  .slideshow-button:hover {
    background-color: #45a049;
  }
  
  .caption,
  .index {
    text-align: center;
    margin-top: 8px;
    font-size: 14px;
    color: #333;
    font-style: italic;
    animation: slideInFromTop 1s ease;
  }
  </style>
  
  