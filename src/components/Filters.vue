<script>
    export default {
        //list of active filters
        props: {
            filters: Array
        },
        //watch when the filters variable changes
        watch: {
            filters(val, oldval){
                this.editFilters()
             }
        },
        methods: {
            //reloads the filters
            editFilters() {
                document.querySelectorAll('input[name="region"]').forEach(i => {
                    i.checked = false
                })   
                document.querySelectorAll('input[name="gender"]').forEach(i => {
                    i.checked = false
                }) 
                document.querySelector('input[id="min"]').value = ''
                document.querySelector('input[id="max"]').value = ''
                this.filters.forEach((v) => {
                    if(v.id == 'min' || v.id == 'max')
                        document.querySelector('input[id=' + v.id + ']').value = v.value
                    else
                    document.querySelector('input[id=' + v.id + ']').checked = true                   
                })
            },
            //checks if age is in correct format
            checkAge() {
                let min = document.querySelector('#min')
                let max = document.querySelector('#max')
                if(parseInt(min.value) > parseInt(max.value)) {
                    max.value = min.value
                }
            },
            onSubmit() {
                this.filters.length = 0
                //get gender
                let radios = document.getElementsByName('gender')
                radios.forEach((g) => {
                    if(g.checked) {
                        let object = {'id': g.id, 'category': 'Pohlavie', 'value': document.querySelector('label[for='+g.id+']').innerHTML}
                            this.filters.push(object)
                    }
                })
                //get regions
                let checkboxes = document.getElementsByName('region')
                checkboxes.forEach((c) => {
                    if(c.checked) {
                        this.filters.push({'id': c.id, 'category': 'Kraj', 'value': document.querySelector('label[for='+c.id+']').innerHTML})
                    }
                })
                //get age range
                let min =  document.querySelector('#min').value
                let max =  document.querySelector('#max').value
                if(min > 0 && min < 2)
                    this.filters.push({'id': 'min', 'category': 'Vek od', 'value': min + ' rok'})
                else if(min > 1 && min < 5)
                    this.filters.push({'id': 'min', 'category': 'Vek od', 'value': min + ' roky'})
                else if(min > 4)
                    this.filters.push({'id': 'min', 'category': 'Vek od', 'value': min + ' rokov'})
                if(max > 0 && max < 2)
                    this.filters.push({'id': 'max', 'category': 'Vek do', 'value': max + ' rok'})
                else if(max > 1 && max < 5)
                    this.filters.push({'id': 'max', 'category': 'Vek do', 'value': max + ' roky'})
                else if(max > 4)
                    this.filters.push({'id': 'max', 'category': 'Vek do', 'value': max + ' rokov'})
                this.$emit('edit-filters', this.filters)
            }
        },
    }

</script>

<template>
    <div class="modal" id="exampleModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Filtrovanie</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form action="" name="filters" class="">
                        <div class="row">
                            <div class="col">
                                <h4>Pohlavie</h4>
                                <div class="form-check">
                                    <input class="form-check-input" type="radio" name="gender" id="male">
                                    <label class="form-check-label" for="male">Pes</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="radio" name="gender" id="female">
                                    <label class="form-check-label" for="female">Fenka</label>
                                </div>
                            </div>
                            <div class="col">
                                <h4>Kraj</h4>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="BL">
                                    <label class="form-check-label" for="BL">Bratislava</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="TA" >
                                    <label class="form-check-label" for="TA">Trnava</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="TC">
                                    <label class="form-check-label" for="TC">Trenčín</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="NI">
                                    <label class="form-check-label" for="NI">Nitra</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="ZI">
                                    <label class="form-check-label" for="ZI">Žilina</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="BC">
                                    <label class="form-check-label" for="BC">Banská Bystrica</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="PV">
                                    <label class="form-check-label" for="PV">Prešov</label>
                                </div>
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" name="region" id="KI">
                                    <label class="form-check-label" for="KI">Košice</label>
                                </div>
                            </div>
                            <div class="col">
                                <h4>Vek</h4>
                                <div class="form-floating ">
                                    <input v-on:change="checkAge" type="number" class="form-control" id="min" min="1" max="15">
                                    <label for="floatingInput">Od</label>
                                </div>
                                <br>
                                <div class="form-floating ">
                                    <input v-on:change="checkAge" type="number" class="form-control" id="max" min="1" max="15">
                                    <label for="floatingInput">Do</label>
                                </div>
                            </div>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" @click="editFilters" data-bs-dismiss="modal">Zrušiť</button>
                    <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="onSubmit">Potvrdiť</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
</style>