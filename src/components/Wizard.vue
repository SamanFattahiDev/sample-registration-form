<template>
  <div class="w-full p-3">
    <div class="w-full">
      <button :disabled="appStore.getCurrentStep===1" type="button" class="btn p-2 disabled:bg-gray-50 disabled:border-none disabled:text-gray-300 rounded-full text-primary hover:text-white bg-white hover:bg-primary transition-all border-2 border-primary">
        <ArrowLeft class="w-6 h-6"></ArrowLeft>
      </button>
    </div>
  </div>
</template>
<script setup lang="ts">
import ArrowLeft from "@/components/icons/ArrowLeft.vue";
import {useAppStore} from "@/stores/index.js";
const appStore = useAppStore()

</script>
