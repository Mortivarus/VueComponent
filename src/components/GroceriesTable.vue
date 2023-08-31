<script setup>
import {ref, computed} from 'vue'

const prodName = ["Brood", "Broccoli", "Krentenbollen", "Noten"]
const prodPrice = [1.00, 0.99, 1.20, 2.99]
const prodQuantity = ref([0, 0, 0, 0])

const prodTotals = computed(()=>{
    let list = []
    for (let i = 0; i < prodName.length; i++) {
        list[i] = (prodPrice[i] * prodQuantity.value[i])
    }
    return list
})

let sumTotal = computed(()=>{
    const reducer = (accumulator, item) => {return accumulator + item}
    return prodTotals.value.reduce(reducer, 0).toFixed(2)
})

</script>

<template>
    <table>
        <tr>
            <th>Product</th>
            <th>Prijs</th>
            <th>Aantal</th>
            <th>Subtotaal</th>
        </tr>
        <tr v-for="i in prodName.length">
            <td>{{ prodName[i-1] }}</td>
            <td>{{ prodPrice[i-1].toFixed(2) }}</td>
            <td><input type="number" v-model="prodQuantity[i-1]"></td>
            <td>{{ prodTotals[i-1].toFixed(2) }}</td>
        </tr>
        <tr>
            <td colspan="3">Totaal</td>
            <td>{{ sumTotal }}</td>
        </tr>
    </table>


</template>

<style scoped>
table{
    display: inline-table;
    border-collapse: collapse;
}

th, td, table{
    border: 1px solid #888;
    padding: 10px;
    font-family: sans-serif;
}

th{
    color: white;
    background-color: black;
    text-align: left;
}

#number, #totalCost, #total{
    text-align: right;
}

</style>