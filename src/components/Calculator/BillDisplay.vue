<template>
   <h2>Bill</h2>
   <div class="flex flex-row justify-between cursor-pointer border-[5px] border-transparent hover:border-grey-200">
      <p class="pl-8 cursor-pointer">€</p>
      <input
         :value="bill"
         @input="emit('update:bill', $event.target.valueAsNumber)"
         type="number"
         placeholder="0"
         class="text-right cursor-pointer outline-0 text-primary font-bold" />
   </div>
</template>
<script setup>
const props = defineProps({
   bill: Number,
})
const emit = defineEmits(["update:bill"])
</script>
