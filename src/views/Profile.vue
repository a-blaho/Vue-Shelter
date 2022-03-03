<script setup>
    import Shelter from '../components/Shelter.vue'
    import Request from '../components/Request.vue'
</script>

<template>
    <div class="container">
        <div class="row">
            <a href="" style="text-decoration: none; color: black;">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-arrow-left" viewBox="0 0 16 16">
                    <path fill-rule="evenodd" d="M15 8a.5.5 0 0 0-.5-.5H2.707l3.147-3.146a.5.5 0 1 0-.708-.708l-4 4a.5.5 0 0 0 0 .708l4 4a.5.5 0 0 0 .708-.708L2.707 8.5H14.5A.5.5 0 0 0 15 8z"/>
                </svg> Späť
            </a>
        </div>
        <br>
        <div class="row">
            <div class="col-sm-6" style="text-align: center">
                <img src="https://via.placeholder.com/400" alt="">
            </div>
            <div class="col-sm-6">
                <h1>Bella</h1>
                <h5>Pohavie: Fenka, Vek: 3 roky</h5>
                <h5>Kraj: Košický</h5>
                <h5>Útulok: <a href="">OZ Košipes</a></h5>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo distinctio fugiat omnis eveniet nostrum eum, culpa veritatis consectetur facilis, iure ullam corrupti nulla cum sequi nihil, dolorum deserunt veniam exercitationem.</p>
                <button class="btn btn-info btn-lg" data-bs-toggle="modal" data-bs-target="#exampleModal">Kontakovať útulok</button>
            </div>
        </div>
    </div>

    <Request/>

</template>