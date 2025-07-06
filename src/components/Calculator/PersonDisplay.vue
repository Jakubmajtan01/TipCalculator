<template>
   <h2 class="pt-8">Number of People</h2>
   <div
      @click="isActive"
      :class="{ 'border-grey-200': isActive }"
      class="flex justify-between items-center border-5 border-transparent hover:border-grey-200 cursor-pointer">
      <img src="/src/images/icon-person.svg" class="w-4 ml-8 cursor-pointer" />
      <div>
         <input
            @input="emit('update:personCount', $event.target.valueAsNumber)"
            class="w-[150px] text-right cursor-pointer outline-0"
            placeholder="1"
            type="number"
            min="1"
            max="30" />
      </div>
   </div>
</template>
<script setup>
const props = defineProps({
   personCount: Number,
})
const emit = defineEmits(["update:personCount"])
</script>
