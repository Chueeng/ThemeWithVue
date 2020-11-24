<template>
  <div id="app" v-bind:class="picked">
    <div class="color-palettes">
      <input
        v-for="color in colors"
        type="radio"
        class="input-color"
        :class="color.value"
        :value="color.value"
        :key="color.index"
        v-model="picked"
      />
    </div>

    <transition name="circle" mode="in-out">
      <card class="box light" v-if="picked === 'light'"></card>
      <card class="box dark" v-else-if="picked === 'dark'"></card>
      <card class="box orange" v-else></card>
    </transition>
  </div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  name: "App",
  data() {
    return {
      picked: "light",
      colors: [
        { id: 1, value: "light" },
        { id: 2, value: "dark" },
        { id: 3, value: "orange" }
      ],
    };
  },
  methods: {
    getColor(picked) {
      this.picked = picked;
    },
  },
   components: {
    Card,
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');
.box {
  font-family: 'Varela Round', sans-serif; 
  z-index: -1;
  align-items: center;
  background-color: var(--background);
  color: var(--color);
  height: 100%;
  justify-content: center;
  position: absolute;
  width: 100%;
}

.circle-enter-active {
  animation: 1s circle reverse;
}
.circle-leave-active {
  animation: 9s circle;
}
@keyframes circle {
  0% {
    clip-path: circle(150% at 150px 90px);
  }
  100% {
    clip-path: circle(0% at 150px 90px);
  }
}

body {
  margin: 0;
}
.light {
  --color: #112d32;
  background:#ECEFF1;
  --background: #ECEFF1;
  --card-color: #f7f7f7;
  --text-color-primary: black;
  --text-color-success: #007a46;
  --text-color-error: #c83825;
  --text-color-warning: #ff6600;
}
.dark {
  --color: #c2c2c2;
   background: #505050;
  --background: #505050;
  --card-color: #323232;
  --text-color-primary: white;
  --text-color-success: #1eb980;
  --text-color-error: #ff6859;
  --text-color-warning: #ffcf44;
  
}
.orange {
  --color: #8e3d35;
  background: #edc7b7;
  --background: #edc7b7;
  --card-color: #f9f3f0;
  --text-color-primary: #8e3d35;
  --text-color-success: #008b52;
  --text-color-error: #e44838;
  --text-color-warning: #ff9900;
}

.input-color {
  outline: none;
  width: 40px;
  height: 40px;
  border-radius: 20px;
  border: 2px solid white;
  padding: 10px;
  margin: 10px;
}
.color-palettes {
  display: flex;
  position: absolute;
  z-index: 1;
  padding: 30px;
}
input[type="radio"] {
  appearance: none;
}
</style>
