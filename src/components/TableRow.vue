<template>
<tr>
    <td tabindex="-1">{{name}}</td>
    <td>
        <editable-cell
            :desc="desc"
            @description-edited="emitNewDescription"
            ></editable-cell>
    </td>
    <td tabindex="-1">{{price}}</td>
    <td tabindex="-1">{{amount}}</td>
    <td tabindex="-1">{{expiration}}</td>
    <button class="buttonRemove"
        @click="emitDeleteItem">
        <svg aria-hidden="true" focusable="false" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
            <path fill="currentColor" d="M268 416h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12zM432 80h-82.41l-34-56.7A48 48 0 0 0 274.41 0H173.59a48 48 0 0 0-41.16 23.3L98.41 80H16A16 16 0 0 0 0 96v16a16 16 0 0 0 16 16h16v336a48 48 0 0 0 48 48h288a48 48 0 0 0 48-48V128h16a16 16 0 0 0 16-16V96a16 16 0 0 0-16-16zM171.84 50.91A6 6 0 0 1 177 48h94a6 6 0 0 1 5.15 2.91L293.61 80H154.39zM368 464H80V128h288zm-212-48h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12z"></path>
        </svg>
    </button>
</tr>
</template>

<script>
import EditableCell from './EditableCell.vue';

export default {
    name: 'TableRow',
    props: {
        id:         { required: true, type: String },
        name:       { required: true, type: String },
        desc:       { required: true, type: String },
        price:      { required: true, type: String },
        amount:     { required: true, type: String },
        expiration: { required: true, type: String }
    },
    components: {
        EditableCell
    },
    methods: {
        emitNewDescription(newDescription) {
            this.$emit('description-edited', this.id, newDescription);
        },
        emitDeleteItem() {
            this.$emit('delete-item', this.id);
        }
    }
}
</script>

<style scoped>

td {
    padding: 1rem;
}

tr {
    position: relative;
}

.buttonRemove{
    width: 1rem;
    height: 1rem;
    opacity: .4;
    position: absolute;
    right: -1.5rem;
    top: 1rem;
}

</style>