<template>
    <div>
    <div class="bg-blue-500 py-1 px-4">
        <p class="text-lg font-bold text-gray-900">Payable Amount</p>
    </div>
        <div class="">
            <table class="min-w-full">
                <colgroup>
                <col span="1" style="width: 20%" />
                <col span="1" style="width: 14%" />
                <col span="1" style="width: 23%" />
                <col span="1" style="width: 23%" />
              </colgroup>
                <thead class="bg-[#1e344e]">
                    <th class="text-left pl-2">For</th>
                    <th class="right-align-td">percentage</th>
                    <th class="right-align-td">Payable</th>
                    <th class="right-align-td">Remaining</th>
                </thead>
                <tbody>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">First <span class="font-bold">3</span> Lakh</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">0</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">0</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">{{ props.totalTaxableAmount }}</td>
                    </tr>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">Next <span class="font-bold">1</span> Lakh</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">5%</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">{{ nextOneLakhTaxableIncome.payableAmount }}</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">{{ nextOneLakhTaxableIncome.remainingAmount }}</td>
                    </tr>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">Next <span class="font-bold">3</span> Lakh</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">10%</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">{{ nextThreeLakhTaxableIncome.payableAmount }}</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">{{ nextThreeLakhTaxableIncome.remainingAmount }}</td>
                    </tr>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">Next <span class="font-bold">4</span> Lakh</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">15%</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">5000</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">1022000</td>
                    </tr>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">Next <span class="font-bold">5</span> Lakh</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">20%</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">5000</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">1022000</td>
                    </tr>
                    <tr>
                        <td class="px-2 py-3 border-b border-gray-500 text-sm">Rest Amount</td>
                        <td class="text-center px-2 py-3 border-b border-gray-500">25%</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">5000</td>
                        <td class="text-right px-2 py-3 border-b border-gray-500">1022000</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from "vue";
const props = defineProps({
    totalTaxableAmount: Number
})

const nextOneLakhTaxableIncome = computed(() => {
    let taxableAmount = props.totalTaxableAmount
    let PayableAmount = 0;
    let remainingAmount = 0;
    PayableAmount = Math.round(taxableAmount * 5 / 100)
        remainingAmount = taxableAmount - PayableAmount
    return {
        "payableAmount": PayableAmount,
        "remainingAmount": remainingAmount
    }
})
const nextThreeLakhTaxableIncome = computed(() => {
    let PayableAmount = 0;
    let remainingAmount = 0;
    if(nextOneLakhTaxableIncome.value.remainingAmount > 0){
        PayableAmount = Math.round(nextOneLakhTaxableIncome.value.remainingAmount * 10 / 100)
        remainingAmount = nextOneLakhTaxableIncome.value.remainingAmount - PayableAmount
    }

    return {
        "payableAmount": PayableAmount,
        "remainingAmount": remainingAmount
    }
})
</script>

<style scoped>

</style>