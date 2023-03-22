<template>
    <td class="px-3 py-2 text-sm w-2/12">
        <span>{{ salary.month }}</span><span>&nbsp;{{ new Date().getFullYear() }}</span>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <input v-model.trim="salaryInfo.grossSalary" type="number" class="bg-transparent focus:outline-none py-2 border border-gray-500 rounded-sm px-3 text-right">
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.basicPercentage" type="number" class="bg-transparent focus:outline-none bg-[#1a2e44] py-2 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="focus:outline-none py-2 bg-gray-600 w-[20%] text-center">
        <input v-model="basicSalary" type="number" class="bg-transparent focus:outline-none py-2 bg-[#1a2e44] px-3 w-[40%] text-right">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.homeRentPercentage" type="number" class="bg-transparent focus:outline-none bg-[#1a2e44] py-2 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="focus:outline-none py-2 bg-gray-600 w-[20%] text-center">
        <input v-model="homeRent" type="number" class="bg-transparent focus:outline-none py-2 bg-[#1a2e44] px-3 w-[40%] text-right">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.medicalPercentage" type="number" class="bg-transparent focus:outline-none bg-[#1a2e44] py-2 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="focus:outline-none py-2 bg-gray-600 w-[20%] text-center">
        <input v-model="medicalAllowance" type="number" class="bg-transparent focus:outline-none py-2 bg-[#1a2e44] px-3 w-[40%] text-right">
        </div>
    </td>
    <td class="text-sm font-light px-2 py-2 capitalize">
        <div class="flex justify-center border border-gray-500 rounded-sm w-full">
        <input v-model.trim="salaryInfo.conveyancePercentage" type="number" class="bg-transparent focus:outline-none bg-[#1a2e44] py-2 px-3 w-[40%]">
        <input v-model="percentage" readonly type="text" class="focus:outline-none py-2 bg-gray-600 w-[20%] text-center">
        <input v-model="salaryInfo.conveyanceAllowance" type="number" class="bg-transparent focus:outline-none py-2 bg-[#1a2e44] px-3 w-[40%] text-right">
        </div>
    </td>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';

const percentage = ref('%')

const { salary } = defineProps({
    salary: Object
})
const salaryInfo = ref({})

onMounted(() => {salaryInfo.value = salary})

// Basic Salary
const basicSalary = computed(() => {
    let getBasicSalary = 0;
    if(salaryInfo.value.grossSalary){
        getBasicSalary = Math.round(salaryInfo.value.grossSalary * salaryInfo.value.basicPercentage / 100)  
    }else{
       getBasicSalary = ''
    }
    return getBasicSalary
})

// Home Rent
const homeRent = computed(() => {
    let getHomeRent = 0;
    getHomeRent = Math.round(salaryInfo.value.grossSalary * salaryInfo.value.homeRentPercentage / 100)
    return getHomeRent
})

// Medical Allowance
const medicalAllowance = computed(() => {
    let getMedicalAllowance = 0;
    getMedicalAllowance = Math.round(salaryInfo.value.grossSalary * salaryInfo.value.medicalPercentage / 100)
    return getMedicalAllowance
})

// watch(salary, currentSalary => {
//     if(currentSalary.grossSalary && currentSalary.grossSalary > 0){
//         salaryInfo.value.basicSalary =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.basicPercentage / 100)
//         salaryInfo.value.homeRent =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.homeRentPercentage / 100)
//         salaryInfo.value.medicalAllowance =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.medicalPercentage / 100)
//         salaryInfo.value.conveyanceAllowance =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.conveyancePercentage / 100)
//     }else {
//         salaryInfo.value.basicSalary = ''
//         salaryInfo.value.homeRent = ''
//         salaryInfo.value.medicalAllowance = ''
//         salaryInfo.value.conveyanceAllowance = ''
//     }
// })

</script>

<style scoped>

</style>