<template>
  <div class="flex flex-col gap-2">
    <VInput
        inputId="email"
        v-model.trim="email"
        :dataType="'email'"
        :error="emailValidationNotMatch"
        class="col-span-12"
        label="Email:"
        placeHolder="Enter Email"
        vname="search"
    ></VInput>
    <span v-if="emailValidationNotMatch" class="text-red-500 text-[12px]">Invalid Email.</span>
  </div>
</template>

<script lang="ts" setup>
import {ref} from "vue";
import VInput from "@/components/utilities/VInput.vue";
import {IStepsPayload} from "@/components/models/IStepsPayload";

const emailValidationNotMatch = ref<Boolean>(false)
const email = ref<string>('')
const emits = defineEmits<{
  (e: 'setPayload', payload: IStepsPayload): void
}>()

function validateInput() {
  if (email.value === '@') {
    emits('setPayload', {key: 'email', value: email.value})
  } else {
    emailValidationNotMatch.value = true
  }
}

defineExpose<{
  validateInput(): void
}>({
  validateInput,
})
</script>

<style scoped>

</style>