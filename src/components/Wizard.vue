<template>
  <div class="w-full p-3">
    <div class="w-full flex items-center justify-between">
      <button id="btn-prev" :disabled="currentStep===1"
              class="btn p-2 disabled:bg-gray-50 disabled:border-none disabled:text-gray-300 rounded-full text-primary hover:text-white bg-white hover:bg-primary transition-all border-2 border-primary"
              type="button" @click="previousStep">
        <ArrowLeft class="w-6 h-6"></ArrowLeft>
      </button>
      <button id="btn-next" :disabled="currentStep ===Object.keys(steps).length"
              class="btn p-2 disabled:bg-gray-50 disabled:border-none disabled:text-gray-300 rounded-full text-primary hover:text-white bg-white hover:bg-primary transition-all border-2 border-primary"
              type="button"
              @click="validateComponent">
        <ArrowLeft class="w-6 h-6 transform rotate-180"></ArrowLeft>
      </button>
    </div>
    <div class="w-full flex  my-2  flex-col gap-2">
      <component :is="computedStep" ref="asyncComponents" @setPayload="validationSuccessful"></component>
    </div>
  </div>
</template>

<script lang="ts" setup>
import ArrowLeft from "@/components/icons/ArrowLeft.vue";
import type {Component} from 'vue'
import {computed, ref} from "vue";
import {IStepsPayload} from "@/components/models/IStepsPayload";
import Username from "@/components/Steps/Username.vue";
import Email from "@/components/Steps/Email.vue";
import Description from "@/components/Steps/Description.vue";

const asyncComponents = ref<Component | null>(null)
let steps = {
  1: Username,
  2: Email,
  3: Description,
}

let currentStep = ref(1)
let computedStep = computed(() => {
  return steps[currentStep.value]
})


// const steps: Record<number, string> = {
//   1: 'Username',
//   2: 'Email',
//   3: 'Description',
// }
// const currentStep = ref(1)
// const asyncStep = defineAsyncComponent({
//   loader: () => import(`./Steps/${steps[computedCurrentStep.value]}.vue`),
// })
// const computedCurrentStep = computed(() => {
//   return currentStep.value
// })
const registrationData = ref<any>({})

function validateComponent() {
  asyncComponents.value.validateInput()
}

function validationSuccessful(data: IStepsPayload | null) {
  registrationData[data.key] = data.value
  setCurrentStep()
}

function setCurrentStep() {
  // here we check if current step component exists in steps
  let currentStepIndex = Object.keys(steps).findIndex(e => e == currentStep.value)
  // here we check that if current component has a next sibling, increment currentStep value
  if (!!steps[currentStepIndex + 2]) {
    // const {setStep} = useAppStore()
    currentStep.value++
    // setStep(currentStep.value)
  }
}

function previousStep() {
  // const {setStep} = useAppStore()
  currentStep.value--
// setStep(currentStep.value)
}
</script>
