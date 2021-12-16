<template>
<modal-add-item
    v-show="isModalAddItemOpen"
    @close-modal="switchModalAddItemOff"
    @add-new-item="addNewItem"
    ></modal-add-item>

<h1>Groceries</h1>

<section class="buttonGroup">
    <button
        @click="switchModalAddItemOn"
        >Add item</button>
    <button
        @click="addNewItem()"
        >Add 1 blank</button>
    <button id="buttonFetch"
        @click="fetchDataAndReplace('http://localhost:3000/items')"
        >Look in the Fridge</button>
</section>

<groceries-table
    :goodsLocal="Goods"
    @table-edited="updateData"
    ></groceries-table>
</template>

<script>
import GroceriesTable from './components/GroceriesTable.vue';
import ModalAddItem from './components/ModalAddItem.vue';
import uniqueId from 'lodash.uniqueid';

export default {
    name: 'App',
    components: {
        GroceriesTable,
        ModalAddItem
    },
    data() {
        return {
            isModalAddItemOpen: false,
            Goods: [
                // { id: uniqueId('row-'), name: 'Apple',  description: 'Red and tasty',            price: '$2',    amount: '2', expiration: 'in 5 days' },
                // { id: uniqueId('row-'), name: 'Milk',   description: '3.5% fats',                price: '$1.5',  amount: '1', expiration: 'in 2 days' },
                // { id: uniqueId('row-'), name: 'Cake',   description: 'With chocolate and cream', price: '$6',    amount: '1', expiration: 'in 3 days' },
            ]
        }
    },
    created() {
        this.fetchDataAndReplace('http://localhost:3000/items')
    },
    methods: {
        fetchDataAndReplace(url) {
            fetch(url)
                .then( res  => res.json() )
                .then( data => {
                    this.Goods.length = 0;
                    for (let i=0; i<data.length; i++) {
                        this.Goods.push(
                            {
                                ...data[i],
                                id: uniqueId('row-'),
                            }
                        )
                    }
                } );
        },
        updateData(updatedGoods) {
            this.Goods = updatedGoods;
        },
        switchModalAddItemOn() {
            this.isModalAddItemOpen = true;
        },
        switchModalAddItemOff() {
            this.isModalAddItemOpen = false;
        },
        addNewItem(newName='---', newDesc='---', newPrice='---', newAmount='---', newExpire='---') {
            this.Goods.push(
                {
                    id: uniqueId('row-'),
                    name: newName,
                    description: newDesc,
                    price: newPrice,
                    amount: newAmount,
                    expiration: newExpire
                }
            )
        }
    }
}
</script>

<style scoped>
.buttonGroup {
    display: grid;
    grid-template-columns: auto auto 1fr auto;
}
#buttonFetch {
    grid-column: 4;
}
</style>
