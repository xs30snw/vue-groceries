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
            @delete-item="deleteItem"
            ></table-row>
    </tbody>
</table>
</template>

<script>
import TableRow from './TableRow.vue';

export default {
    name: 'GroceriesTable',
    props: {
        goodsLocal: { required: true, type: Array },
    },
    components: {
        TableRow
    },
    data() {
        return {
            Goods: this.goodsLocal
        };
    },
    methods: {
        emitEditedTable() {
            this.$emit('table-edited', this.Goods);
        },
        setNewDescription(rowId, newDescription) {
            var row = this.Goods.find(item=>item.id===rowId);
            if (row) {
                row.description = newDescription;
                this.emitEditedTable();
            }
        },
        deleteItem(rowId) {
            var index = this.Goods.findIndex(item=>item.id===rowId);
            if (index>=0 && index<this.Goods.length) {
                this.Goods.splice(index, 1);
                this.emitEditedTable();
            }
        }
    },
    // mounted() {   
    //     console.log(this.Goods);
    // }
}
</script>

<style>
table, th, td {
    border: 1px solid red;
    border-collapse: collapse;
}
td:last-child {
    border: 1px solid white;
}
</style>