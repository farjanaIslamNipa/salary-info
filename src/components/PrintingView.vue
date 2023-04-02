<template>
  <div id="printArea" class="bg-gray-100 p-5 border absolute left-0 right-0 top-0 text-black w-full">
    <div class="bg-white px-4 pt-6 pb-10 mx-auto print-preview-width">
      <div class="flex justify-between gap-4">
          <div class="space-y-1">
            <p class="text-[15px] font-bold">Name: <span class="ml-1 font-semibold capitalize">{{ props.employeeName }}</span></p>
            <p class="text-[15px] font-bold">Designation: <span class="ml-1 font-semibold capitalize">{{ props.designation }}</span></p>
            <p class="text-[15px] font-bold">Department: <span class="ml-1 font-semibold capitalize">{{ props.department }}</span></p>
          </div>
          <div>
            <button @click="print" class="bg-teal-600 text-white font-semibold rounded-sm px-6 py-1 mx-1">Print</button>
            <button @click="props.closePreview" class="bg-gray-600 text-white font-semibold rounded-sm px-6 py-1 mx-1">Cancel</button>
          </div>
      </div>

      <div class="mt-3">
        <div class="py-1 capitalize">
          <h3 class="text-xl font-bold text-center text-gray-700">salary information</h3>
        </div>
        <div class="overflow-x-auto">
            <table class="w-[954px] lg:w-full">
                <colgroup>
                  <col span="1" style="width: 16%" />
                  <col span="1" style="width: 12%" />
                  <col span="1" style="width: 18%" />
                  <col span="1" style="width: 18%" />
                  <col span="1" style="width: 18%" />
                  <col span="1" style="width: 18%" />
                </colgroup>
                <thead>
                    <tr class="border-t border-b">
                    <th scope="col" class="left-align-td">Month</th>
                    <th scope="col" class="left-align-td text-center">Gross Salary</th>
                    <th scope="col" class="left-align-td text-center">Basic</th>
                    <th scope="col" class="left-align-td text-center">Home rent</th>
                    <th scope="col" class="left-align-td text-center">Medical</th>
                    <th scope="col" class="left-align-td text-center">Conveyance</th>
                  </tr>
                </thead>
                <tbody>
                    <tr
                    v-for="salary in salaryData"
                    :key="salary.id"
                    class="border-b print-preview-input"
                  >
                    <SalaryTableRow :salary="salary" />
                  </tr>
                </tbody>
                <tfoot>
                  <tr class="">
                    <td scope="col" class="left-align-td">Total</td>
                    <td scope="col" class="right-align-td text-center">
                      {{ props.getSum.totalGrossSalary }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.getSum.totalBasicSalary }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.getSum.totalHomeRent }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.getSum.totalMedicalAllowance }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.getSum.totalConveyanceAllowance }}
                    </td>
                  </tr>
                  <tr>
                    <td colspan="2" class="left-align-td">Tax Exemption</td>
                    <td scope="col" class="right-align-td">0</td>
                    <td scope="col" class="right-align-td">
                      {{ props.homeRentTaxExemption }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.medicalTaxExemption }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.conveyanceTaxExemption }}
                    </td>
                  </tr>
                  <tr>
                    <td colspan="2" class="left-align-td">Taxable</td>
                    <td scope="col" class="right-align-td">{{ props.taxableBasicSalary }}</td>
                    <td scope="col" class="right-align-td">
                      {{ props.taxableHomeRent }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.taxableMedicalAllowance }}
                    </td>
                    <td scope="col" class="right-align-td">
                      {{ props.taxableConveyanceAllowance }}
                    </td>
                  </tr>
                </tfoot>
            </table>
        </div>
      </div>
      <!-- <div class="grid grid-cols-2 gap-2 mt-10">
        <div class="mt-5">
        <table class="mb-3">
            <tbody>
                <tr>
                    <td><p class="font-semibold text-[15px] py-1">Festive Bonus One:</p></td>
                    <td><p class="font-semibold text-[15px] pl-3 py-1 text-right">{{ props.festiveBonusOne ? props.festiveBonusOne : 0 }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-semibold text-[15px] py-1">Festive Bonus Two:</p></td>
                    <td><p class="font-semibold text-[15px] pl-3 py-1 text-right">{{ props.festiveBonusOne ? props.festiveBonusOne : 0 }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-bold text-[16px] py-1">Total Taxable Income:</p></td>
                    <td><p class="font-bold text-[16px] pl-3 py-1 text-right">{{ props.totalTaxableAmount }}</p></td>
                </tr>
                
            </tbody>
        </table>
        <hr class=" mr-5">
        <table class="mt-3">
            <tbody>
                <tr>
                    <td><p class="font-bold text-[16px] py-1">Total Payable Amount:</p></td>
                    <td><p class="font-bold text-[16px] pl-3 py-1 text-right">{{ props.totalPayable }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-semibold text-[15px] py-1">Total Investment Amount:</p></td>
                    <td><p class="font-semibold text-[15px] pl-3 py-1 text-right">{{ props.investedAmount ? props.investedAmount : 0 }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-semibold text-[15px] py-1">Allowable Investment Amount:</p></td>
                    <td><p class="font-semibold text-[15px] pl-3 py-1 text-right">{{ props.allowedInvestedAmount ? props.allowedInvestedAmount : 0 }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-semibold text-[15px] py-1">Redemption for investment:</p></td>
                    <td><p class="font-semibold text-[15px] pl-3 py-1 text-right">{{ props.applicableDiscount ? props.applicableDiscount : 0 }}</p></td>
                </tr>
                <tr>
                    <td><p class="font-bold text-[15px] py-1">AIT:</p></td>
                    <td><p class="font-bold text-[15px] pl-3 py-1 text-right">{{ props.aitAmount ? props.aitAmount : 0 }}</p></td>
                </tr>
            </tbody>
        </table>
            <div class="p-2 mt-3 bg-gray-100 actual-payable-amount-bg mr-4">
                <p class="font-bold text-lg">Actual Total Payable Amount: <span>{{ props.actualTotalPayableAmount }}</span></p>
            </div>
        </div>
        <div>
          <div class="py-1 mt-4 lg:mt-0">
            <p class="text-lg font-bold">Payable Amount</p>
          </div>
          <div class="overflow-x-auto">
            <table class="w-full">
              <thead class="border-t border-b">
                <th class="text-left pl-2">For</th>
                <th class="left-align-td text-center">Rate</th>
                <th class="right-align-td">Payable</th>
                <th class="right-align-td">Remaining</th>
              </thead>
              <tbody>
                <tr>
                  <td class="px-2 py-3 border-b text-sm">
                    First <span class="font-bold">3</span> Lakh
                  </td>
                  <td class="text-center px-2 py-3 border-b">0</td>
                  <td class="text-right px-2 py-3 border-b">0</td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.remainingAmountAfterFirstThreeLakh }}
                  </td>
                </tr>
                <tr>
                  <td class="px-2 py-3 border-b text-sm">
                    Next <span class="font-bold">1</span> Lakh
                  </td>
                  <td class="text-center px-2 py-3 border-b">5%</td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextOneLakhTaxableIncome.payableAmount }}
                  </td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextOneLakhTaxableIncome.remainingAmount }}
                  </td>
                </tr>
                <tr>
                  <td class="px-2 py-3 border-b text-sm">
                    Next <span class="font-bold">3</span> Lakh
                  </td>
                  <td class="text-center px-2 py-3 border-b">10%</td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextThreeLakhTaxableIncome.payableAmount }}
                  </td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextThreeLakhTaxableIncome.remainingAmount }}
                  </td>
                </tr>
                <tr>
                  <td class="px-2 py-3 border-b text-sm">
                    Next <span class="font-bold">4</span> Lakh
                  </td>
                  <td class="text-center px-2 py-3 border-b">15%</td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextFourLakhTaxableIncome.payableAmount }}
                  </td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextFourLakhTaxableIncome.remainingAmount }}
                  </td>
                </tr>
                <tr>
                  <td class="px-2 py-3 border-b text-sm">
                    Next <span class="font-bold">5</span> Lakh
                  </td>
                  <td class="text-center px-2 py-3 border-b">20%</td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextFiveLakhTaxableIncome.payableAmount }}
                  </td>
                  <td class="text-right px-2 py-3 border-b">
                    {{ props.nextFiveLakhTaxableIncome.remainingAmount }}
                  </td>
                </tr>
                <tr>
                  <td class="px-2 py-3 text-sm font-bold">Rest Amount</td>
                  <td class="text-center px-2 py-3">25%</td>
                  <td class="text-right px-2 py-3">
                    {{ props.restTaxableIncome }}
                  </td>
                  <td class="text-right px-2 py-3">0</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import SalaryTableRow from "./SalaryTableRow.vue";

const props = defineProps({
  closePreview: Function,
  salaryData: Object,
  noPrint: String,
  employeeName: String,
  designation: String,
  department: String,
  getSum: Object,
  homeRentTaxExemption: Number,
  medicalTaxExemption: Number,
  conveyanceTaxExemption: Number,
  taxableBasicSalary: Number,
  taxableHomeRent: Number,
  taxableMedicalAllowance: Number,
  taxableConveyanceAllowance: Number,
  festiveBonusOne: Number,
  festiveBonusTwo: Number,
  totalTaxableAmount: Number,
  remainingAmountAfterFirstThreeLakh: Number,
  nextOneLakhTaxableIncome: Object,
  nextThreeLakhTaxableIncome: Object,
  nextFourLakhTaxableIncome: Object,
  nextFiveLakhTaxableIncome: Object,
  restTaxableIncome: Number,
  totalPayable: Number,
  investedAmount: Number,
  allowedInvestedAmount: Number,
  applicableDiscount: Number,
  aitAmount: Number,
  actualTotalPayableAmount: Number,
});

const print = () => {
  document.getElementById(props.noPrint).className += " noPrint";
  window.print();
};

console.log(props.taxData, "data");
</script>

<style scoped></style>
