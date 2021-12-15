<template>
<tr>
    <td tabindex="-1">{{name}}</td>
    <td>
        <editable-cell
            :id="id"
            :desc="desc"
            @description-edited="emitNewDescription"
            ></editable-cell>
    </td>
    <td tabindex="-1">{{price}}</td>
    <td tabindex="-1">{{amount}}</td>
    <td tabindex="-1">{{expiration}}</td>
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
        emitNewDescription(rowId, newDescription) {
            this.$emit('description-edited', rowId, newDescription);
        }
    }
}
</script>

<style>

</style>