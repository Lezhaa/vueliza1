<template>
  <div id="app" @click="incrementCounter">
    <!-- Counter Component -->
    <div class="counter">
      <h2>Nur Haliza</h2>
      <p>Count: {{ count }}</p>
      <button @click.stop="manualIncrement">Click</button> <!-- stop modifier untuk mencegah double click -->
    </div>

    <!-- Box Color Changer -->
    <div class="color-changer">
      <h2>Box Color Changer</h2>
      <div :style="boxStyle" class="color-box"></div>
      <button v-for="color in colors" :key="color" @click.stop="changeColor(color)">
        {{ color }}
      </button>
    </div>

    <!-- Image Carousel -->
    <div class="carousel">
      <h2>Image Carousel</h2>
      <img :src="images[currentImageIndex]" class="carousel-image" />
      <div class="carousel-controls">
        <button @click.stop="prevImage">Back</button>
        <button @click.stop="nextImage">Next</button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      // Global Counter state
      count: 0,

      // Box color changer state
      currentColor: 'red',
      colors: ['red', 'blue', 'green', 'yellow'],

      // Carousel state
      currentImageIndex: 0,
      images: [
        'https://i.pinimg.com/736x/b6/bd/ba/b6bdba7c51b6f33b030c55620e263771.jpg',
        'https://i.pinimg.com/736x/9f/7d/01/9f7d01afb8838e73df312a784a61e33a.jpg',
        'https://i.pinimg.com/736x/44/2c/f9/442cf9053a9c2b196d13d8694108e3a6.jpg'
      ]
    };
  },
  computed: {
    boxStyle() {
      return {
        width: '100px',
        height: '100px',
        backgroundColor: this.currentColor,
        margin: '10px auto'
      };
    }
  },
  methods: {
    // Global Counter increment function for entire app except button
    incrementCounter() {
      this.count++;
    },

    // Manual increment function for button click
    manualIncrement() {
      this.count++; // Function for the manual button increment
    },

    // Change box color function
    changeColor(color) {
      this.currentColor = color;
    },

    // Carousel functions
    nextImage() {
      this.currentImageIndex =
        (this.currentImageIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentImageIndex =
        (this.currentImageIndex - 1 + this.images.length) % this.images.length;
    }
  }
};
</script>

<style scoped>
.counter, .color-changer, .carousel, .another-counter {
  margin-bottom: 20px;
  text-align: center;
}

.color-box {
  width: 100px;
  height: 100px;
  margin: 10px auto;
  border: 2px solid #000;
}

.carousel-image {
  width: 333px;
  height: 333px;
}

.carousel-controls button {
  margin: 0 5px;
}
</style>
