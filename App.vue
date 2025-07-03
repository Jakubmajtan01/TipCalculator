<template>
   <div class="bg-grey-200 max-w-screen mx-auto h-screen">
      <div class="flex text-center justify-center pb-12 pt-[10%] tracking-[1rem] text-primary font-bold text-2xl">
         <img src="/src/images/logo.svg" />
      </div>
      <div class="grid grid-cols-2 mx-auto justify-between p-8 border border-white bg-white rounded-3xl w-[50%] h-[55%]">
         <div class="m-4">
            <h2>Bill</h2>
            <div class="flex flex-row justify-between mt-4 cursor-pointer border-[5px] border-transparent hover:border-grey-200">
               <p class="pl-8 cursor-pointer text-primary">€</p>
               <input
                  v-model.number="bill"
                  type="Number"
                  placeholder="0"
                  class="text-right cursor-pointer outline-0 text-primary font-bold" />
            </div>
            <div class="mt-14">
               <h2 class="mb-4">Select Tip %</h2>
               <div class="grid grid-cols-3 grid-rows-2 text-white gap-4 border-5 border-hidden">
                  <div v-for="tips in tip" :key="tips.tipValue" class="">
                     <button
                        @click=";(selectedTip = selectedTip === tips.tipValue ? 0 : tips.tipValue), (customTip = 0)"
                        :class="[
                           ' w-[120px] h-[50px] rounded-xl cursor-pointer hover:bg-grey-200 hover:text-primary ',
                           selectedTip === tips.tipValue ? 'bg-grey-200 text-primary' : 'bg-primary',
                        ]">
                        {{ tips.tipName }}%
                     </button>
                  </div>

                  <input
                     v-model.number="customTip"
                     @input="selectedTip = 0"
                     class="w-[120px] rounded-xl cursor-pointer border-5 border-transparent text-primary text-center hover:border-grey-200 hover:border-solid outline-0"
                     placeholder="CUSTOM" />
               </div>
            </div>
            <h2 class="pt-14">Number of People</h2>
            <div class="flex justify-between items-center border-5 border-transparent hover:border-grey-200 cursor-pointer">
               <img src="/src/images/icon-person.svg" class="w-4 m-6 cursor-pointer" />
               <div>
                  <input
                     v-model.number="personCount"
                     type="number"
                     class="w-[150px] text-right cursor-pointer outline-0"
                     placeholder="1"
                     min="1"
                     max="30" />
               </div>
            </div>
         </div>
         <div class="flex flex-col gap-18 border w-full bg-green rounded-3xl bg-primary border-white pt-16">
            <div class="mx-16 flex justify-between">
               <div class="flex flex-col">
                  <p class="text-white">Tip amount</p>
                  <p class="text-grey-400">/person</p>
               </div>
               <p class="text-grn text-5xl pl-16 block">{{ personTip.toFixed(2) }}€</p>
            </div>
            <div class="mx-16 flex justify-between">
               <div class="flex flex-col">
                  <p class="text-white">Total</p>
                  <p class="text-grey-400">/person</p>
               </div>
               <p class="text-grn text-5xl pl-16">{{ finalBill.toFixed(2) }}€</p>
            </div>
            <button
               @click="resetValue"
               class="flex justify-center border-0 bg-grey-400 mx-auto w-[80%] h-[15%] mt-16 items-center text-2xl text-primary text-opacity-70 hover:bg-grey-200 cursor-pointer">
               RESET
            </button>
         </div>
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
   if (personCount.value < 1) return 0
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
