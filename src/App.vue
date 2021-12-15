<template>
<EditableCell />
</template>

<script>
import EditableCell from './components/EditableCell.vue'

export default {
    name: 'App',
    components: {
        EditableCell
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}
#app {
    min-height: 100vh;
    display: grid;
    place-items: center;
}
</style>
