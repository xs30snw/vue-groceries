<template>
<div id="modalAddItem">
    
    <form>

        <h2>Add New Item</h2>

        <div>
            <div>
                <label>
                    <span>Name:</span>
                    <input type="text" v-model.lazy.trim="name">
                </label>
            </div>
            <div>
                <label>
                    <span>Description:</span>
                    <input type="text" v-model.lazy.trim="description">
                </label>
            </div>
            <div>
                <label>
                    <span>Price:</span>
                    <input type="text" v-model.lazy.trim="price">
                </label>
            </div>
            <div>
                <label>
                    <span>Amount:</span>
                    <input type="text" v-model.lazy.trim="amount">
                </label>
            </div>
            <div>
                <label>
                    <span>Expiration:</span>
                    <input type="text" v-model.lazy.trim="expiration">
                </label>
            </div>
        </div>

        <div>
            <button @click="emitAddNewItem">
                Add
            </button>
            <button @click="emitCloseModal">
                Cancel
            </button>
        </div>

    </form>
</div>
</template>

<script>
export default {
    name: 'ModalAddItem',
    data() {
        return {
            name: '',
            description: '',
            price: '',
            amount: '',
            expiration: ''
        }
    },
    methods: {
        emitCloseModal() {
            this.$emit('close-modal');
        },
        emitAddNewItem() {
            this.$emit('add-new-item',
                this.name,
                this.description,
                this.price,
                this.amount,
                this.expiration);
            this.name = this.description = this.price = this.amount = this.expiration = '';
            this.emitCloseModal();
        }
    }
}
</script>

<style scoped>
#modalAddItem {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    display: grid;
    place-items: center;

    background-color: rgba(0, 0, 0, 0.568);
    z-index: 2;
}

form {
    background-color: white;
}
</style>>