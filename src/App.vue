<template>
<table role="grid">
    <tbody>
        <!-- TABLE HEADERS -->
        <tr>
            <th tabindex="-1">Name</th>
            <th tabindex="-1">Description</th>
            <th tabindex="-1">Price</th>
            <th tabindex="-1">Amount</th>
            <th tabindex="-1">Expiration</th>
        </tr>

        <!-- TABLE ROWS from Goods-->
        <table-row v-for="item in Goods" 
            :key        ="item.id"
            :id         ="item.id"
            :name       ="item.name"
            :desc       ="item.description"
            :price      ="item.price"
            :amount     ="item.amount"
            :expiration ="item.expiration"
            @description-edited="setNewDescription"
            ></table-row>
    </tbody>
</table>
</template>

<script>
import TableRow from './components/TableRow.vue';
import uniqueId from 'lodash.uniqueid';

export default {
    name: 'App',
    components: {
        TableRow
    },
    data() {
        return {
            Goods: [
                { id: uniqueId('row-'), name: 'Apple',  description: 'Red and tasty',            price: '$2',    amount: '2', expiration: 'in 5 days' },
                { id: uniqueId('row-'), name: 'Milk',   description: '3.5% fats',                price: '$1.5',  amount: '1', expiration: 'in 2 days' },
                { id: uniqueId('row-'), name: 'Cake',   description: 'With chocolate and cream', price: '$6',    amount: '1', expiration: 'in 3 days' },
            ]
        };
    },
    methods: {
        setNewDescription(rowId, newDescription) {
            var row = this.Goods.find(item=>item.id===rowId);
            if (row) row.description = newDescription;
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
#app {
    min-height: 100vh;
    display: grid;
    place-items: center;
}
</style>
