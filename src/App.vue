<template>
   <div class="bg-grey-200 max-w-screen mx-auto h-screen">
      <div class="flex text-center justify-center pb-12 pt-[10%] tracking-[1rem] text-primary font-bold text-2xl">
         <img src="/src/images/logo.svg" />
      </div>
      <div>
         <Calculator v-model:bill="bill" v-model:tip="tip" v-model:personCount="personCount" @reset="resetValue" />
      </div>
   </div>
</template>
<script setup>
import { watch, ref } from "vue"
import Calculator from "/src/components/Calculator/Calculator.vue"

const bill = ref(0)
const personCount = ref(1)
const tip = ref(0)
const customTip = ref(0)

watch(personCount, (vperson) => {
   if (vperson < 1) {
      alert("Can't be zero!")
      personCount.value = 1
   } else if (vperson > 99) {
      alert("Cant be that many!")
      personCount.value = 1
   }
})
function resetValue() {
   bill.value = 0
   personCount.value = 1
   tip.value = 0
   customTip.value = 0
}
</script>
