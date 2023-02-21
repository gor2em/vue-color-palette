
<script setup>
import { onMounted, reactive } from 'vue';
import Palette from './components/Palette.vue';

const state = reactive({
  colors: [],
  maxPaletteBoxes: 8
})

const handleGeneratePalette = () => {
  state.colors = []
  for (let index = 0; index < state.maxPaletteBoxes; index++) {

    let randomHexCode = Math.floor(Math.random() * 0xffffff).toString(16);
    randomHexCode = `#${randomHexCode.padStart(6, "0")}`;

    state.colors.push({
      code: randomHexCode
    })
  }

}

onMounted(() => handleGeneratePalette())

</script>
<template>
  <div class="min-h-screen bg-black flex items-center justify-center">

    <transition name="fade" appear>

      <div class="py-4 px-8 flex flex-col space-y-8">
        <h1 class="text-4xl font-bold text-white">Random Hex Generator</h1>
        <Palette :colors="state.colors" />
        <button @click.prevent="handleGeneratePalette"
          class="w-full my-8 bg-cyan-600 text-white px-10 py-3 tracking-widest rounded-md text-sm hover:opacity-60 transition-all duration-500 outline-none border-none font-medium active:bg-rose-600">Refresh</button>
      </div>

    </transition>

  </div>
</template>
<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>