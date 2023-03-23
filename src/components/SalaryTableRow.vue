<template>
    <td class="px-3 py-2 text-sm w-2/12">
        <span>{{ salary.month }}</span><span>&nbsp;{{ (new Date().getFullYear()) - 1 }}</span>
    </td>
    <td class="common-td">
        <input v-model.trim="salaryInfo.grossSalary" type="number" class="bg-transparent focus:outline-none py-2 border border-gray-500 rounded-sm px-3 text-right">
    </td>
    <td class="common-td">
        <div class="input-group-wrapper">
        <input v-model.trim="salaryInfo.basicPercentage" type="number" class="common-input">
        <input v-model="percentage" readonly type="text" class="percentage-input">
        <input v-model="salaryInfo.basicSalary" readonly type="number" class="common-input">
        </div>
    </td>
    <td class="common-td">
        <div class="input-group-wrapper">
        <input v-model.trim="salaryInfo.homeRentPercentage" type="number" class="common-input">
        <input v-model="percentage" readonly type="text" class="percentage-input">
        <input v-model="salaryInfo.homeRent" readonly type="number" class="common-input">
        </div>
    </td>
    <td class="common-td">
        <div class="input-group-wrapper">
        <input v-model.trim="salaryInfo.medicalPercentage" type="number" class="common-input">
        <input v-model="percentage" readonly type="text" class="percentage-input">
        <input v-model="salaryInfo.medicalAllowance" readonly type="number" class="common-input">
        </div>
    </td>
    <td class="common-td">
        <div class="input-group-wrapper">
        <input v-model.trim="salaryInfo.conveyancePercentage" type="number" class="common-input">
        <input v-model="percentage" readonly type="text" class="percentage-input">
        <input v-model="salaryInfo.conveyanceAllowance" readonly type="number" class="common-input">
        </div>
    </td>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const percentage = ref('%')

const { salary } = defineProps({
    salary: Object
})
const salaryInfo = ref({})

onMounted(() => {salaryInfo.value = salary})

watch(salary, currentSalary => {
    if(currentSalary.grossSalary && currentSalary.grossSalary > 0){
        salaryInfo.value.basicSalary =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.basicPercentage / 100)
        salaryInfo.value.homeRent =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.homeRentPercentage / 100)
        salaryInfo.value.medicalAllowance =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.medicalPercentage / 100)
        salaryInfo.value.conveyanceAllowance =  Math.round(salaryInfo.value.grossSalary * salaryInfo.value.conveyancePercentage / 100)
    }else {
        salaryInfo.value.basicSalary = ''
        salaryInfo.value.homeRent = ''
        salaryInfo.value.medicalAllowance = ''
        salaryInfo.value.conveyanceAllowance = ''
    }
})


</script>

<style scoped>

</style>