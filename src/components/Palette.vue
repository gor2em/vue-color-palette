<script setup>
import { ref } from 'vue';

defineProps({
    colors: Array
});

let isColorCopied = ref(false)

const copyHexCode = (hexCode) => {
    navigator.clipboard.writeText(hexCode).then(() => {
        isColorCopied.value = true;

        setTimeout(() => isColorCopied.value = false, 1000)
    }).catch(() => alert("Failed!"))
}

</script>
<template>
    <div class="grid grid-cols-8 gap-8">
        <div class="col-span-4 md:col-span-2 h-32 w-32 rounded-lg cursor-pointer transition-all duration-50 hover:scale-95"
            v-for="color in colors" :key="color.code" :style="`background:${color.code}`" @click="copyHexCode(color.code)">
            <div class="flex flex-col items-center justify-around h-full group z-50">
                <span class="block text-center text-xs">
                    {{ color.code }}
                </span>
                <span class="hidden group-hover:block opacity-100 z-20 text-white font-bold text-xl animate-pulse">{{
                    isColorCopied ? "Copied!" : "Copy." }}</span>
            </div>
        </div>
    </div>
</template>
<style scoped></style>