<template>
<h1>Groceries</h1>
<button>Add item</button>
<groceries-table 
    :goodsLocal="Goods"
    @table-edited="updateData"
    ></groceries-table>
</template>

<script>
import GroceriesTable from './components/GroceriesTable.vue';
import uniqueId from 'lodash.uniqueid';

export default {
    name: 'App',
    components: {
        GroceriesTable
    },
    data() {
        return {
            Goods: [
                { id: uniqueId('row-'), name: 'Apple',  description: 'Red and tasty',            price: '$2',    amount: '2', expiration: 'in 5 days' },
                { id: uniqueId('row-'), name: 'Milk',   description: '3.5% fats',                price: '$1.5',  amount: '1', expiration: 'in 2 days' },
                { id: uniqueId('row-'), name: 'Cake',   description: 'With chocolate and cream', price: '$6',    amount: '1', expiration: 'in 3 days' },
            ]
        }
    },
    methods: {
        updateData(updatedGoods) {
            this.Goods = updatedGoods;
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}
*:focus {
    outline: dotted 2px black;
    outline-offset: 2px;
}
html {
    font-size: 18px;
}
body {
    min-height: 100vh;
    display: grid;
    place-items: center;
}
table, th, td {
    border: 1px solid red;
    border-collapse: collapse;
}
</style>
