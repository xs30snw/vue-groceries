<template>
<div class="editableCell">
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
        desc: { required: true, type: String },
    },
    data() {
        return {
            isEditing: false,
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
            this.$emit('description-edited', this.value);
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
.editableCell {
    display: flex;
}
span {
    position: relative;
}
span::after{
    background-image: url('../assets/edit-regular.svg');
    background-position: center;
    background-repeat: no-repeat;
    background-size: 1rem;
    content: ' ';
    width: 1rem;
    height: 1rem;
    opacity: .4;
    position: absolute;
    right: -1.5rem;
    top: 0;
}

span,
input {
    width: 100%;
}
span,
input {
    margin-right: 1.5rem;
}
input {
    font-size: 1rem;
    font-family: 'Times New Roman', Times, serif;
    border: none;
}

</style>