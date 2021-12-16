<template>
<div id="modalWrapper" class="center">
    
    <form class="flexColumn">

        <h2>Add New Item</h2>

        <div class="flexColumn formFields">
            <div>
                <label class="flexColumn formFieldsItem">
                    <span>Name:</span>
                    <input type="text" v-model.lazy.trim="name">
                </label>
            </div>
            <div>
                <label class="flexColumn formFieldsItem">
                    <span>Description:</span>
                    <input type="text" v-model.lazy.trim="description">
                </label>
            </div>
            <div>
                <label class="flexColumn formFieldsItem">
                    <span>Price:</span>
                    <input type="text" v-model.lazy.trim="price">
                </label>
            </div>
            <div>
                <label class="flexColumn formFieldsItem">
                    <span>Amount:</span>
                    <input type="text" v-model.lazy.trim="amount">
                </label>
            </div>
            <div>
                <label class="flexColumn formFieldsItem">
                    <span>Expiration:</span>
                    <input type="text" v-model.lazy.trim="expiration">
                </label>
            </div>
        </div>

        <div>
            <button @click.prevent="emitAddNewItem">
                Add
            </button>
            <button @click.prevent="emitCloseModal">
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
#modalWrapper {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    background-color: hsla(0, 0%, 0%, 0.568);
    z-index: 2;
}
form {
    background-color: hsl(0, 0%, 100%);
    width: 376px;
    padding: 1rem;

    row-gap: 1.5rem;    
}
.formFields {
    row-gap: 1rem;
}
.formFieldsItem {    
    row-gap: .4rem;
}
</style>>