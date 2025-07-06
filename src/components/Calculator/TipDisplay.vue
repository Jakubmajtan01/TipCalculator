<template>
   <div class="pt-12">
      <h2>Select Tip %</h2>
      <div class="grid grid-cols-3 grid-rows-2 text-white gap-4 border-5 border-hidden">
         <div v-for="tips in tip" :key="tips.tipValue" class="">
            <button
               @click="selectTip(tips.tipValue)"
               :class="[
                  ' w-[120px] p-3 rounded-xl cursor-pointer hover:bg-grey-200 hover:text-primary ',
                  selectedTip === tips.tipValue ? 'bg-grey-200 text-primary' : 'bg-primary',
               ]">
               {{ tips.tipName }}%
            </button>
         </div>
         <input
            v-model.number="customTip"
            @input="handleCustomTip"
            type="number"
            class="w-[120px] rounded-xl cursor-pointer border-5 border-transparent text-primary text-center hover:border-grey-200 hover:border-solid outline-0"
            placeholder="CUSTOM" />
      </div>
   </div>
</template>
<script setup>
import { ref, watch } from "vue"

const tip = ref([
   {
      tipName: "5",
      tipValue: 5,
   },
   {
      tipName: "10",
      tipValue: 10,
   },
   {
      tipName: "15",
      tipValue: 15,
   },
   {
      tipName: "20",
      tipValue: 20,
   },
   {
      tipName: "25",
      tipValue: 25,
   },
])

const props = defineProps({
   tip: Number,
})
const emit = defineEmits(["update:tip"])

const customTip = ref(0)
const selectedTip = ref(props.tip ?? 0)

function selectTip(value) {
   selectedTip.value = selectedTip.value === value ? 0 : value
   customTip.value = 0
   emit("update:tip", selectedTip.value)
}

function handleCustomTip() {
   selectedTip.value = 0
   emit("update:tip", customTip.value)
}

watch(
   () => props.tip,
   (resetValue) => {
      selectedTip.value = resetValue
      if (resetValue === 0) {
         customTip.value = 0
      }
   }
)
</script>
