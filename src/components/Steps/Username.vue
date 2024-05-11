<template>
  <div class="flex flex-col gap-2">
    <VInput
        inputId="username"
        v-model.trim="username"
        :dataType="'text'"
        :error="userNameValidationNotMatch"
        class="col-span-12"
        label="Username:"
        placeHolder="Enter Username"
        vname="search"
    ></VInput>
    <span v-if="userNameValidationNotMatch" class="text-red-500 text-[12px]">Invalid Username.</span>
  </div>
</template>

<script lang="ts" setup>
import {ref} from "vue";
import VInput from "@/components/utilities/VInput.vue";
import {IStepsPayload} from "@/components/models/IStepsPayload";

const userNameValidationNotMatch = ref<Boolean>(false)
const username = ref<string>('')
const emits = defineEmits<{
  (e: 'setPayload', payload: IStepsPayload): void
}>()

function validateInput() {
  if (username.value === 'hello') {
    emits('setPayload', {key: 'userName', value: username.value})
  } else {
    userNameValidationNotMatch.value = true
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