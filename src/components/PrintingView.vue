<template>
    <div id="printArea" class="bg-white p-5 border absolute left-0 right-0 top-0 w-full text-black">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Facilis, quis ipsa. Reprehenderit fuga dolor dolores, minus neque deleniti iure vitae.
        <button @click="props.closePreview">cancel</button>
        <button @click="print">Print</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    closePreview: Object,
    salaryData: Object,
    noPrint: String
})

const print = () => {
    document.getElementById(props.noPrint).className += " noPrint";
    window.print();
};

console.log(props.noPrint, 'data');
</script>

<style scoped>

</style>