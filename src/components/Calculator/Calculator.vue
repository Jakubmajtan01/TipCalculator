<template>
   <div class="grid grid-cols-2 mx-auto justify-between p-8 border border-white bg-white rounded-3xl w-[50%] h-[55%]">
      <div class="flex flex-col gap-8 pr-8">
         <BillDisplay :bill="props.bill" @update:bill="emit('update:bill', $event)" />
         <TipDisplay :tip="props.tip" @update:tip="emit('update:tip', $event)" />
         <PersonDisplay :personCount="props.personCount" @update:personCount="emit('update:personCount', $event)" />
      </div>
      <OutputDisplay :bill="props.bill" :tip="props.tip" :personCount="props.personCount" @reset="emit('reset')" />
   </div>
</template>
<script setup>
import BillDisplay from "/src/components/Calculator/BillDisplay.vue"
import TipDisplay from "/src/components/Calculator/TipDisplay.vue"
import PersonDisplay from "/src/components/Calculator/PersonDisplay.vue"
import OutputDisplay from "/src/components/Calculator/OutputDisplay.vue"

const props = defineProps({
   bill: Number,
   tip: Number,
   personCount: Number,
})
const emit = defineEmits(["update:bill", "update:tip", "update:personCount"])
</script>
