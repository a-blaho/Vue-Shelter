<script>
    export default {
        props: {
            filters: Array
        },
        methods: {
            onDelete(filter) {
                this.$emit('delete-filter', filter)
            }
        }
    }
</script>

<template>
    <div class="row justify-content-md-left">
        <div v-for="filter in this.filters" class="col-sm-auto">
            <button v-on:click="onDelete(filter)" class="btn btn-primary" style="border-radius: 20px; margin-top: 10px;">{{filter.category}}: {{filter.value}} 
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                    <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                </svg>
            </button>
        </div>
    </div>
</template>