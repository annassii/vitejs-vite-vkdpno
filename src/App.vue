<template>
  <div @click="showMenu">
    <!-- Only show the menu if 'isMenuVisible' is true -->
    <div v-if="isMenuVisible" :style="menuPositionStyle" class="radial-menu">
      <!-- Display 4 options inside the radial menu -->
      <div
        v-for="(option, index) in options"
        :key="index"
        :style="optionStyles[index]"
        class="menu-item"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// reactive variables
const isMenuVisible = ref(false); // track if the menu is visible or hidden
const menuPosition = ref({ x: 0, y: 0 }); // store the x, y position of the click
const options = ['Option 1', 'Option 2', 'Option 3', 'Option 4'];

function showMenu(event) {
  menuPosition.value = { x: event.clientX, y: event.clientY }; // Get mouse click coordinates
  isMenuVisible.value = true; // Make menu visible
}

// positions of the options in a circle
const optionStyles = [
  { position: 'absolute', top: '0px', left: '50%' },
  { position: 'absolute', top: '50%', right: '0px' },
  { position: 'absolute', bottom: '0px', left: '50%' },
  { position: 'absolute', top: '50%', left: '0px' },
];
</script>

<style>
.radial-menu {
  position: relative;
}

.menu-item {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-size: 12px;
}
</style>
