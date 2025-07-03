<template>
   <h2>Select Tip %</h2>
   <div class="grid grid-cols-3 grid-rows-2 text-white gap-4 border-5 border-hidden">
      <div v-for="tips in tip" :key="tips.tipValue" class="">
         <button
            @click=";(selectedTip = selectedTip === tips.tipValue ? 0 : tips.tipValue), (customTip = 0)"
            :class="[
               ' w-[120px] rounded-xl cursor-pointer hover:bg-grey-200 hover:text-primary ',
               selectedTip === tips.tipValue ? 'bg-grey-200 text-primary' : 'bg-primary',
            ]">
            {{ tips.tipName }}%
         </button>
      </div>
      <input
         v-model="customTip"
         @input="selectedTip = 0"
         class="w-[120px] rounded-xl cursor-pointer border-5 border-transparent text-primary text-center hover:border-grey-200 hover:border-solid outline-0"
         placeholder="CUSTOM" />
   </div>
</template>
<script setup></script>
