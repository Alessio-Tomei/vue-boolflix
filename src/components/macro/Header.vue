<template>
<header>
    <div class="container">
        <div class="row row-cols-2 align-items-center">
            <div class="col">
                <h1>BOOLFLIX</h1>
            </div>
            <div class="col ms_searchBar-container">
                <SearchBar @searchUp="textUp"/>
            </div>
        </div>
    </div>
</header>
</template>

<script>
import SearchBar from '../commons/SearchBar.vue';

export default {
    name: 'Header',
    components: { 
        SearchBar, 
    },
    methods: {
        textUp: function(text) {
            this.$emit('searchUp', text)
        }
    }
}
</script>

<style lang="scss" scoped>
@import "../../assets/style/variables.scss";

header {
    background-color: $bg-color;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    .row {
        height: $header-height;
    }
    h1 {
        margin: 0px;
        color: $theme-color;
    }
    .ms_searchBar-container {
        text-align: center;
    }
}

</style>