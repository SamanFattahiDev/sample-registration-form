<template>
  <div class="w-full    flex items-center  ">
    <div v-for="step in headerSteps" :class="{'border-b-2 border-b-green-500 !text-black':appStore.getCurrentStep===step.stepId}"
         class=" w-1/3 flex items-center text-gray-300 justify-center p-3 ">
      <span>{{ step.title }}</span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {ref} from "vue";
import {useAppStore} from "@/stores";

interface IHeaderSteps {
  stepId: number,
  title: string,
  width: string
}
const appStore = useAppStore()
const headerSteps = ref<IHeaderSteps[]>([
  {
    stepId: 1,
    title: 'Username',
    width: '33%'
  },
  {
    stepId: 2,
    title: 'Email',
    width: '66%'
  },
  {
    stepId: 3,
    title: 'Description',
    width: '100%'
  },
])


</script>

<style scoped>

</style>
