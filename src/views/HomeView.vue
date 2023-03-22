<template>
  <div class="pt-5 pb-10 app-primary-bg app-primary-text h-screen">
    <div class="grid grid-cols-12 gap-4 px-20">
      <div class="col-span-9">
        <div class="app-secondary-bg">
          <div class="py-1 bg-gold capitalize">
            <h3 class="text-xl font-bold text-center text-gray-700">
              salary information
              {{ testCal }}
            </h3>
          </div>
          <div class="">
            <table class="min-w-full">
              <colgroup>
                <col span="1" style="width: 16%" />
                <col span="1" style="width: 12%" />
                <col span="1" style="width: 18%" />
                <col span="1" style="width: 18%" />
                <col span="1" style="width: 18%" />
                <col span="1" style="width: 18%" />
              </colgroup>
              <thead class="app-primary-bg">
                <tr>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">Month</th>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                    Gross Salary
                  </th>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">Basic</th>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                    Home rent
                  </th>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                    Medical
                  </th>
                  <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                    Conveyance
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="salary in salaryData"
                  :key="salary.id"
                  class="border-b border-gray-500"
                >
                  <SalaryTableRow :salary="salary" />
                </tr>
              </tbody>
              <tfoot>
                <tr class="bg-blue-500">
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-left">Total</td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ getSum.totalGrossSalary }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ getSum.totalBasicSalary }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ getSum.totalHomeRent }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ getSum.totalMedicalAllowance }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ getSum.totalConveyanceAllowance }}
                  </td>
                </tr>
                <tr class="bg-blue-900">
                  <td colspan="2" class="text-sm font-bold px-2 py-2 text-left">
                    Tax Exemption
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">-0</td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ homeRentTaxExemption }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ medicalTaxExemption }}
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    {{ conveyanceTaxExemption }}
                  </td>
                </tr>
                <tr class="bg-gray-600">
                  <td colspan="2" class="text-sm font-bold px-2 py-2 text-left">
                    Taxable
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">-0</td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    -30000
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">
                    10000
                  </td>
                  <td scope="col" class="text-sm font-bold px-2 py-2 text-right">5000</td>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
      </div>
      <div class="col-span-3">
        <div class="app-secondary-bg p-6">
        
        </div>
      </div>
    </div>
  </div>

</template>

<script setup>
import sourceData from "../../data.json";
import SalaryTableRow from "@/components/SalaryTableRow.vue";
import { ref, computed } from "vue";

const salaryData = ref([...sourceData]);

const getSum = computed(() => {
  let totalGrossSalary = 0;
  let totalBasicSalary = 0;
  let totalHomeRent = 0;
  let totalMedicalAllowance = 0;
  let totalConveyanceAllowance = 0;
  
  for(let i = 0; i< salaryData.value.length; i++) {
    totalGrossSalary += salaryData.value[i].grossSalary
    totalBasicSalary += salaryData.value[i].basicSalary
    totalHomeRent += salaryData.value[i].homeRent
    totalMedicalAllowance += salaryData.value[i].medicalAllowance
    totalConveyanceAllowance += salaryData.value[i].conveyanceAllowance
  }

  return {
    "totalGrossSalary": totalGrossSalary,
    "totalBasicSalary": totalBasicSalary,
    "totalHomeRent": totalHomeRent,
    "totalMedicalAllowance": totalMedicalAllowance,
    "totalConveyanceAllowance": totalConveyanceAllowance
  }
})

// Calculation Home Rent Tax Exemption 
const homeRentTaxExemption = computed(() => {
  let getHomeRentTaxExemption = Math.round(getSum.value.totalBasicSalary * 50 / 100)
      if(getHomeRentTaxExemption < 300000){
         return getHomeRentTaxExemption
      }else{
        return 300000
      }
})

// Calculation Medical Tax Exemption 
const medicalTaxExemption = computed(() => {
  let getMedicalTaxExemption = Math.round(getSum.value.totalBasicSalary * 10 / 100)
      if(getMedicalTaxExemption < 120000){
         return getMedicalTaxExemption
      }else{
        return 120000
      }
})

// Calculation Conveyance Exemption 
const conveyanceTaxExemption = computed(() => {
  let getConveyanceTaxExemption = Math.round(getSum.value.totalBasicSalary * 5 / 100)
      if(getConveyanceTaxExemption < 30000){
         return getConveyanceTaxExemption
      }else{
        return 30000
      }
})


</script>

<style scoped></style>
