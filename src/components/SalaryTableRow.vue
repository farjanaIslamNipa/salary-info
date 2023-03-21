<template>
    <td class="px-3 py-2 text-sm w-2/12">
        <span>{{ salary.month }}</span><span>&nbsp;{{ new Date().getFullYear() }}</span>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <input v-model.trim="salaryInfo.grossSalary" type="text" class="bg-transparent focus:outline-none py-3 border border-gray-500 rounded-sm px-3">
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.basicPercentage" type="text" class="bg-transparent focus:outline-none bg-[#1a2e44] py-3 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="bg-transparent focus:outline-none py-3 bg-gray-700 px-3 w-[20%] text-center">
        <input v-model="salaryInfo.basicSalary" type="text" class="bg-transparent focus:outline-none py-3 bg-[#1a2e44] px-3 w-[40%]">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.homeRentPercentage" type="text" class="bg-transparent focus:outline-none bg-[#1a2e44] py-3 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="bg-transparent focus:outline-none py-3 bg-gray-700 px-3 w-[20%] text-center">
        <input v-model="salaryInfo.homeRentAmount" type="text" class="bg-transparent focus:outline-none py-3 bg-[#1a2e44] px-3 w-[40%]">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.medicalPercentage" type="text" class="bg-transparent focus:outline-none bg-[#1a2e44] py-3 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="bg-transparent focus:outline-none py-3 bg-gray-700 px-3 w-[20%] text-center">
        <input v-model="salaryInfo.medicalAmount" type="text" class="bg-transparent focus:outline-none py-3 bg-[#1a2e44] px-3 w-[40%]">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.conveyancePercentage" type="text" class="bg-transparent focus:outline-none bg-[#1a2e44] py-3 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="bg-transparent focus:outline-none py-3 bg-gray-700 px-3 w-[20%] text-center">
        <input v-model="salaryInfo.conveyanceAmount" type="text" class="bg-transparent focus:outline-none py-3 bg-[#1a2e44] px-3 w-[40%]">
        </div>
    </td>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue';

const percentage = ref('%')

const {salary} = defineProps({
    salary: Object
})

const salaryInfo = ref({})

onMounted(() => {salaryInfo.value = salary})

const getBasicSalary = computed(() => {
    return Math.round(salaryInfo.value.grossSalary * salaryInfo.value.basicPercentage / 100)
})
 
console.log(getBasicSalary.value, 'get salary');
watch([salaryInfo.value.grossSalary, salaryInfo.value.basicPercentage], (currentValue) => {
   if(salaryInfo.value.grossSalary && salaryInfo.value.basicPercentage && currentValue){
    salaryInfo.value.basicSalary = getBasicSalary.value
   }
});

// Calculating home rent
// const getHomeRent = computed(() => {
//     return Math.round(grossSalary.value * homeRentPercentage.value / 100)
// })

// watch([grossSalary, homeRentPercentage], (currentValue) => {
//    if(grossSalary.value && homeRentPercentage.value && currentValue){
//     homeRentAmount.value = getHomeRent.value
//    }else {
//         homeRentAmount.value = ''
//     }
// });

// Calculating medical amount
// const getMedicalAmount = computed(() => {
//     return Math.round(grossSalary.value * medicalPercentage.value / 100)
// })

// watch([grossSalary, medicalPercentage], (currentValue) => {
//    if(grossSalary.value && medicalPercentage.value && currentValue){
//     medicalAmount.value = getMedicalAmount.value
//    }else {
//     medicalAmount.value = ''
//     }
// });

// Calculating medical amount
// const getConveyanceAmount = computed(() => {
//     return Math.round(grossSalary.value * conveyancePercentage.value / 100)
// })

// watch([grossSalary, conveyancePercentage], (currentValue) => {
//    if(grossSalary.value && conveyancePercentage.value && currentValue){
//     conveyanceAmount.value = getConveyanceAmount.value
//    }else {
//     conveyanceAmount.value = ''
//     }
// });

</script>

<style scoped>

</style>