<template>
  <div class="flex flex-col gap-2">
    <VInput
        v-model.trim="description"
        class="col-span-12"
        data-type="text"
        inputId="description"
        label="Description"
        placeHolder="Write Your Description"
    ></VInput>
    <span v-if="isDescriptionBalanced===true" class="text-green-500 text-[12px]">The text is balanced.</span>
    <span v-else-if="isDescriptionBalanced===false" class="text-red-500 text-[12px]">The text is not balanced.</span>
    <button class="btn bg-green-500 text-white p-2 rounded-xl" type="button" @click="isBalanced">Check Balance</button>
  </div>
</template>
<script>
import VInput from "@/components/utilities/VInput.vue";

export default {
  components: {VInput},
  data() {
    return {
      description: '',
      isDescriptionBalanced: null,
      specialCharacters: ['{', '[', '(', ')', ']', '}']
    }
  },
  methods: {
    isBalanced() {
      if (this.description) {
        let counter = 0
        let descriptionArray = this.description.split(' ')
        for (let i = 0; i < descriptionArray.length; i++) {
          this.specialCharacters.forEach((char) => {
            if (descriptionArray[i].includes(char)) {
              counter++
            }
          })
        }
        if (counter % 2 === 0) {
          this.isDescriptionBalanced = true
        } else {
          this.isDescriptionBalanced = false
        }
      }
    }
  }
}
</script>


<style scoped>

</style>