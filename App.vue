<template>
   <div class="bg-grey-200 max-w-screen mx-auto h-screen">
      <div class="flex text-center justify-center pb-12 pt-[10%] tracking-[1rem] text-primary font-bold text-2xl">
         <img src="/src/images/logo.svg" />
      </div>
      <div class="grid grid-cols-2 mx-auto justify-between p-8 border border-white bg-white rounded-3xl w-[50%] h-[55%]">
         <Calculator></Calculator>
      </div>
   </div>
</template>
<script setup>
import { ref, computed, watch } from "vue"
import Calculator from "/src/components/Calculator/Calculator.vue"

const selectedTip = ref(0)
const personCount = ref(1)
const bill = ref(0)
const customTip = ref(0)
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

const activeTip = computed(() => {
   return customTip.value ? customTip.value : selectedTip.value
})
const currentTip = computed(() => {
   return (bill.value * activeTip.value) / 100
})

const personTip = computed(() => {
   if (personCount.value < 1) return (bill.value = 0)
   else {
      return currentTip.value / personCount.value
   }
})
const finalBill = computed(() => {
   if (personCount.value < 1) return 0
   else {
      return (bill.value + personTip.value * personCount.value) / personCount.value
   }
})

function resetValue() {
   bill.value = 0
   personCount.value = 1
   selectedTip.value = 0
   customTip.value = 0
}

watch(personCount, (vperson) => {
   if (vperson < 1) {
      alert("Can't be zero!")
      personCount.value = 1
   } else if (vperson > 99) {
      alert("Cant be that many!")
      personCount.value = 1
   }
})
</script>
