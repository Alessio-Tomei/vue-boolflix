<template>
<div class="search-bar">
    <input type="text" 
    v-model="inputSearch" 
    @keyup.enter="$emit('searchUp', inputSearch);"
    placeholder="Titolo film o serie tv"
    >
    <button @click="$emit('searchUp', inputSearch)">Cerca</button>
    <button @click="resetInput">Reset</button>
</div>
</template>

<script>
export default {
    name: 'SearchBar',
    data() {
        return {
            inputSearch: '',
        }
    },
    methods: {
        resetInput: function() {
            console.log('reset');
            this.inputSearch = '';
        }
    }
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/variables.scss";

.search-bar {
   
    input {
        width: 40%;
        padding: 0px 20px;
        border-radius: 5px;
        border: none;
        outline: none;
    }
    button {
        width: 100px;
        padding: 0px 20px;
        border-radius: 5px;
        border: none;
        outline: none;
        margin-left: 10px;
    }
}

</style>