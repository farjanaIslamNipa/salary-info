<template>
  <div class="pt-5 pb-10 app-primary-bg app-primary-text h-screen">
    <div class="grid grid-cols-12 gap-4 lg:px-20 px-5">
      <div class="col-span-9">
        <div class="app-secondary-bg">
          <div class="py-1 bg-gold capitalize">
            <h3 class="text-xl font-bold text-center text-gray-700">
              salary information
            </h3>
          </div>
          <div class="overflow-x-auto">
            <table class="w-[1000px] xl:w-full">
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
                  <th scope="col" class="footer-left-align-td">
                    Month
                  </th>
                  <th scope="col" class="footer-left-align-td">
                    Gross Salary
                  </th>
                  <th scope="col" class="footer-left-align-td">
                    Basic
                  </th>
                  <th scope="col" class="footer-left-align-td">
                    Home rent
                  </th>
                  <th scope="col" class="footer-left-align-td">
                    Medical
                  </th>
                  <th scope="col" class="footer-left-align-td">
                    Conveyance
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="salary in salaryData"
                  :key="salary.id"
                  class="border-b border-gray-600"
                >
                  <SalaryTableRow :salary="salary" />
                </tr>
              </tbody>
              <tfoot>
                <tr class="bg-blue-500">
                  <td scope="col" class="footer-left-align-td">Total</td>
                  <td scope="col" class="footer-right-align-td">
                    {{ getSum.totalGrossSalary }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ getSum.totalBasicSalary }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ getSum.totalHomeRent }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ getSum.totalMedicalAllowance }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ getSum.totalConveyanceAllowance }}
                  </td>
                </tr>
                <tr class="bg-blue-900">
                  <td colspan="2" class="footer-left-align-td">
                    Tax Exemption
                  </td>
                  <td scope="col" class="footer-right-align-td">0</td>
                  <td scope="col" class="footer-right-align-td">
                    {{ homeRentTaxExemption }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ medicalTaxExemption }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ conveyanceTaxExemption }}
                  </td>
                </tr>
                <tr class="bg-gray-600">
                  <td colspan="2" class="footer-left-align-td">
                    Taxable
                  </td>
                  <td scope="col" class="footer-right-align-td">{{ taxableBasicSalary }}</td>
                  <td scope="col" class="footer-right-align-td">
                    {{ taxableHomeRent }}
                  </td>
                  <td scope="col" class="footer-right-align-td">
                    {{ taxableMedicalAllowance }}
                  </td>
                  <td scope="col" class="footer-right-align-td">{{ taxableConveyanceAllowance }}</td>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
        <div class="mt-6">
        <div class="flex justify-between items-center">
            <div class="flex gap-3 items-center">
            <div>
                <label class="text-sm block" for="">Festive Bonus One</label>
                <input v-model="festiveBonusOne" type="number" class="block focus:outline-none app-secondary-bg py-1 px-3 border border-gray-500 rounded-sm">
            </div>
            <div>
                <label class="text-sm block" for="">Festive Bonus Two</label>
                <input v-model="festiveBonusTwo" type="number" class="block focus:outline-none app-secondary-bg py-1 px-3 border border-gray-500 rounded-sm">
            </div>
            </div>
            <div>
            <p class="pr-2 font-semibold"><span class="text-lg text-blue-400">Total Taxable Amount :&nbsp;</span> <span class="text-xl">{{ totalTaxableAmount }}</span></p>
            </div>
        </div>
      </div>
        <!-- <TotalTaxableSection /> -->
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
// import TotalTaxableSection from "@/components/TotalTaxableSection.vue";
import { ref, computed } from "vue";

const salaryData = ref([...sourceData]);
const festiveBonusOne = ref('')
const festiveBonusTwo = ref('')

const getSum = computed(() => {
  let totalGrossSalary = 0;
  let totalBasicSalary = 0;
  let totalHomeRent = 0;
  let totalMedicalAllowance = 0;
  let totalConveyanceAllowance = 0;
  
  for(let i = 0; i< salaryData.value.length; i++) {
    if(salaryData.value[i].grossSalary > 0){
      totalGrossSalary += salaryData.value[i].grossSalary
      totalBasicSalary += salaryData.value[i].basicSalary
      totalHomeRent += salaryData.value[i].homeRent
      totalMedicalAllowance += salaryData.value[i].medicalAllowance
      totalConveyanceAllowance += salaryData.value[i].conveyanceAllowance
    }
  }

  return {
    "totalGrossSalary": totalGrossSalary,
    "totalBasicSalary": totalBasicSalary,
    "totalHomeRent": totalHomeRent,
    "totalMedicalAllowance": totalMedicalAllowance,
    "totalConveyanceAllowance": totalConveyanceAllowance
  }
})

// Calculation of Tax Exemption 
// Home Rent
const homeRentTaxExemption = computed(() => {
  let getHomeRentTaxExemption = Math.round(getSum.value.totalBasicSalary * 50 / 100)
      if(getHomeRentTaxExemption < 300000){
         return getHomeRentTaxExemption
      }else{
        return 300000
      }
})

// Medical
const medicalTaxExemption = computed(() => {
  let getMedicalTaxExemption = Math.round(getSum.value.totalBasicSalary * 10 / 100)
      if(getMedicalTaxExemption < 120000){
         return getMedicalTaxExemption
      }else{
        return 120000
      }
})

// Conveyance 
const conveyanceTaxExemption = computed(() => {
      if(getSum.value.totalConveyanceAllowance < 30000){
         return 0
      }else{
        return 30000 
      }
})

// Calculation of Taxable Amount
// Basic Salary
const taxableBasicSalary = computed(() => {
  let taxableBasic = 0
  if(getSum.value.totalBasicSalary){
    taxableBasic =  getSum.value.totalBasicSalary - 0
  }
  return taxableBasic;
})

// Home Rent
const taxableHomeRent = computed(() => {
  return getSum.value.totalHomeRent - homeRentTaxExemption.value
})

// Medical
const taxableMedicalAllowance = computed(() => {
  return getSum.value.totalMedicalAllowance - medicalTaxExemption.value
})

// Conveyance
const taxableConveyanceAllowance = computed(() => {
  return getSum.value.totalConveyanceAllowance - conveyanceTaxExemption.value
})

// Calculation of Total Taxable Amount
const totalTaxableAmount = computed(() => {
  let getTotalTaxableAmount = 0
  if(taxableBasicSalary.value){
    getTotalTaxableAmount = taxableBasicSalary.value +
    taxableHomeRent.value +
    taxableMedicalAllowance.value +
    taxableConveyanceAllowance.value +
    (+festiveBonusOne.value) +
    (+festiveBonusTwo.value)
  }

  if((festiveBonusOne.value && festiveBonusOne.value > 0) || (festiveBonusTwo.value && festiveBonusTwo.value > 0)){
    getTotalTaxableAmount = taxableBasicSalary.value +
                              taxableHomeRent.value +
                              taxableMedicalAllowance.value +
                              taxableConveyanceAllowance.value +
                              (+festiveBonusOne.value) +
                              (+festiveBonusTwo.value)
    }else{
      getTotalTaxableAmount = taxableBasicSalary.value +
                              taxableHomeRent.value +
                              taxableMedicalAllowance.value +
                              taxableConveyanceAllowance.value 
    }
  return getTotalTaxableAmount
})


</script>

<style scoped></style>
