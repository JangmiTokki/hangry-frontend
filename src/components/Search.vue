<template>
    <div class="row" id="search">
    <form class="form-inline my-2 my-lg-0" >
      <input @input="updateSearch" class="form-control mr-sm-2" type="text" placeholder="Search for food" id="search-bar" :value="searchTerm">
      <button class="btn btn-primary my-2 my-sm-0" type="submit">Search</button>
    </form>
    </div>

</template>

<script>
export default {
    name: 'search',
    props: {
        searchTerm: String
    },
    methods: {
        updateSearch(event){
            this.$emit("updateSearchTerm", event.target.value)
        }
    }
}
</script>

<style>
    #search{
       margin: 5rem;
       justify-content: center;
    }
</style>