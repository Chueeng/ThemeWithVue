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

    <transition name="move-down">
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
        { id: 3, value: "orange" },
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
  min-height: 100vh;
  width: 100%;
  background-color: var(--background);
  position: absolute;
  font-family: 'Varela Round', sans-serif;
}

.move-down-enter-active {
  animation: 5s down-enter;
}
.move-down-leave-active {
  animation: 5s down-leave;
}
@keyframes down-enter {
  0% {
    /* clip-path: inset(0 0 100% 0); */
     clip-path: inset(0 100% 0 0);
  }
  100% {
    clip-path: inset(0);
  }
}
@keyframes down-leave {
  0% {
    clip-path: inset(0);
  }
  100% {
    /* clip-path: inset(100% 0 0 0); */
    clip-path: inset(0 0 0 100%);
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
