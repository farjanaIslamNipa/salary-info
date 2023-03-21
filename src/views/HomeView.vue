<template>
  <div class="pt-5 pb-10 app-primary-bg app-primary-text">
      <div class="container mx-auto app-secondary-bg">
          <div class="py-1 bg-gold capitalize">
              <h3 class="text-xl font-bold text-center text-gray-700">salary information</h3>
          </div>
      <div class="">
        <table class="min-w-full">
          <colgroup>
          <col span="1" style="width: 14%;">
          <col span="1" style="width: 10%;">
          <col span="1" style="width: 16%;">
          <col span="1" style="width: 16%;">
          <col span="1" style="width: 16%;">
          <col span="1" style="width: 16%;">
          <col span="1" style="width: 12%;">
        </colgroup>
          <thead class="app-primary-bg">
            <tr>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Month
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Gross Salary
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Basic
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Home rent
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Medical
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Conveyance
              </th>
              <th scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Others
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="salary in salaryData" :key="salary.id" class="border-b border-gray-500">
              <SalaryTableRow :salary="salary" />
            </tr>
           
          </tbody>
          <tfoot>
            <tr class="bg-blue-500">
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Total
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Gross Salary
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Basic
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Home rent
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                10000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                5000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                0
              </td>
            </tr>
            <tr class="bg-blue-900">
              <td colspan="2" class="text-sm font-bold px-2 py-2 text-left">
                Tax Exemption
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                -0
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                -30000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                10000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                5000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                0
              </td>
            </tr>
            <tr class="bg-gray-600">
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Taxable
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Gross Salary
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Basic
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                Home rent
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                10000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                5000
              </td>
              <td scope="col" class="text-sm font-bold px-2 py-2 text-left">
                0
              </td>
            </tr>
          </tfoot>
        </table>
      </div>
      </div>
  </div>
</template>

<script setup>
import sourceData from '../../data.json'
import SalaryTableRow from '@/components/SalaryTableRow.vue';
import { ref } from 'vue';

const salaryData = ref([...sourceData])


</script>

<style scoped>

</style>