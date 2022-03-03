<script>
import Home from './views/Home.vue'
import Shelters from './views/Shelters.vue'
import Navbar from './components/Navbar.vue'
import NotFound from './views/NotFound.vue'
import Profile from './views/Profile.vue'
import Contact from './views/Contact.vue'

const routes = {
  '/': Home,
  '/shelters': Shelters,
  '/profile': Profile,
  '/contact': Contact
}

export default {
    data() {
        return {
            currentPath: window.location.hash
        };
    },
    computed: {
        currentView() {
            return routes[this.currentPath.slice(1) || "/"] || NotFound;
        }
    },
    mounted() {
        window.addEventListener("hashchange", () => {
            this.currentPath = window.location.hash;
        });
    },
    components: { Navbar }
}
</script>

<template>
  <Navbar/>
  <component :is="currentView" />
</template>

<style>
 
</style>