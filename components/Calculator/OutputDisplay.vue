<template>
   <div class="pr-14 text-2xl leading-12 text-grey-400">
      <div class="pt-8 text-grey-400"></div>
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
</template>
<script setup></script>
