<template>
  <div class="flex flex-col gap-2">
    <VTextArea
        v-model.trim="description"
        :dataType="'email'"
        :error="descriptionValidationNotMatch"
        class="col-span-12"
        inputId="description"
        label="Description"
        placeHolder="Write Your Description"
        vname="search"
    ></VTextArea>
    <span v-if="descriptionValidationNotMatch" class="text-red-500 text-[12px]">Invalid Description.</span>
  </div>
</template>

<script lang="ts" setup>
import {ref} from "vue";
import {IStepsPayload} from "@/components/models/IStepsPayload";
import VTextArea from "@/components/utilities/VTextArea.vue";

const descriptionValidationNotMatch = ref<Boolean>(false)
const description = ref<string>('')
const emits = defineEmits<{
  (e: 'setPayload', payload: IStepsPayload): void
}>()

function validateInput() {
  if (description.value === '@') {
    emits('setPayload', {key: 'description', value: description.value})
  } else {
    descriptionValidationNotMatch.value = true
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