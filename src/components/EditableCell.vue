<template>
<div class="editable-text">
    <span tabindex  ="-1" 
            role    ="button"
            v-if    ="!isEditing" 
            @click  ="switchEditingOn">
        {{desc}}
    </span>
    <input tabindex ="-1"
            ref     ="editingInput"
            v-if    ="isEditing" 
            v-model.lazy.trim   ="value"
            @blur   ="switchEditingOff">
</div>
</template>

<script>
export default {
    name: 'EditableCell',    
    props: {
        id:   { required: true, type: String },
        desc: { required: true, type: String },
    },
    data() {
        return {
            isEditing: false,
            ide: this.id,
            value: this.desc,
        };
    },
    methods: {
        switchEditingOn() {
            this.isEditing = true;
            this.focusEditingInput();
        },
        switchEditingOff() {
            this.isEditing = false;
            this.$emit('description-edited', this.ide, this.value);
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
</style>