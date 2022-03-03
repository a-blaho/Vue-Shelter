<script setup>
  import Dog from '../components/Dog.vue'
  import Filters from '../components/Filters.vue'
  import FilterButton from '../components/FilterButton.vue'
</script>
<script>
  export default {
      data() {
          return {  
            filters: []
          }
      },
      methods: {
      deleteFilter(filter) {
        let filters = this.filters.filter((f) => !(f.category == filter.category && f.value == filter.value))
        this.filters = filters
      },
      editFilters(filters) {
        this.filters = filters
      }
    }
  }
</script>

<template>
    <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <div class="input-group">
          <input type="text" class="form-control" aria-describedby="button-addon2" placeholder="Vyhľadávanie">
          <button class="btn btn-outline-secondary" type="button" id="button-addon2">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
              <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
            </svg>
          </button>
        </div>
      </div>
      <div class="col" style="text-align:right">
        <button data-bs-toggle="modal" data-bs-target="#exampleModal" class="btn btn-primary">Filter <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-filter" viewBox="0 0 16 16">
          <path d="M6 10.5a.5.5 0 0 1 .5-.5h3a.5.5 0 0 1 0 1h-3a.5.5 0 0 1-.5-.5zm-2-3a.5.5 0 0 1 .5-.5h7a.5.5 0 0 1 0 1h-7a.5.5 0 0 1-.5-.5zm-2-3a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 0 1h-11a.5.5 0 0 1-.5-.5z"/>
          </svg>
        </button>
      </div>
    </div>
    <Filters @edit-filters="editFilters" :filters="filters"/>
    <div class="row">
      <FilterButton @delete-filter="deleteFilter" :filters="filters"/>
    </div>
    <div class="row">
      <div v-for="i in 12" class="col-lg-3 col-md-4 col-sm-6">
        <Dog/>
      </div>
    </div>

  </div>
</template>