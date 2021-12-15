<template>
<div class="editable-text">
    <span tabindex="-1" role="button"
            v-if="!isEditing" 
            @click="switchEditingOn">
        {{value}}
    </span>
    <input tabindex="-1"
            ref="editingInput"
            v-if="isEditing" 
            v-model="value"
            @blur="switchEditingOff">
</div>
</template>

<script>
export default {
    name: 'EditableCell',
    data() {
        return {
            isEditing: false,
            value: 'Switch'
        };
    },
    methods: {
        switchEditingOn() {
            console.log('Editing mode is on');
            this.isEditing = true;
            this.focusEditingInput();
        },
        switchEditingOff() {
            console.log('Editing mode is off');
            this.isEditing = false;
        },
        focusEditingInput() {
            this.$nextTick(() => {
                const editingInputRef = this.$refs.editingInput;
                editingInputRef.focus();
            });
        },
    }
}
</script>

<style scoped>
*:focus {
    outline: dotted 2px black;
    outline-offset: 2px;
}
</style>
