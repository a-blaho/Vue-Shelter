<script>
    let genders = ['Pes', 'Fenka']
    let regions = ['Bratislava', 'Trnava', 'Trenčín', 'Banská Bystrica', 'Žilina', 'Prešov', 'Košice', 'Nitra']
    let maleNames = ["Max", "Buddy", "Charlie", "Jack", "Cooper", "Rocky", "Toby", "Tucker", "Jake", "Bear", "Duke", "Teddy", "Oliver", "Riley", "Bailey", "Bentley", "Milo", "Buster", "Cody", "Dexter", "Winston", "Murphy", "Leo", "Lucky", "Oscar", "Louie", "Zeus", "Henry", "Sam", "Harley", "Baxter", "Gus", "Sammy", "Jackson", "Bruno", "Diesel", "Jax", "Gizmo", "Bandit", "Rusty", "Marley", "Jasper", "Brody", "Roscoe", "Hank", "Otis", "Bo", "Joey", "Beau", "Ollie", "Tank", "Shadow", "Peanut", "Hunter", "Scout", "Blue", "Rocco", "Simba", "Tyson", "Ziggy", "Boomer", "Romeo", "Apollo", "Ace", "Luke", "Rex", "Finn", "Chance", "Rudy", "Loki", "Moose", "George", "Samson", "Coco", "Benny", "Thor", "Rufus", "Prince", "Chester", "Brutus", "Scooter", "Chico", "Spike", "Gunner", "Sparky", "Mickey", "Kobe", "Chase", "Oreo", "Frankie", "Mac", "Benji", "Bubba", "Champ", "Brady", "Elvis", "Copper", "Cash", "Archie", "Walter"]
    let femaleNames = ["Bella", "Lucy", "Daisy", "Molly", "Lola", "Sophie", "Sadie", "Maggie", "Chloe", "Bailey", "Roxy", "Zoey", "Lily", "Luna", "Coco", "Stella", "Gracie", "Abby", "Penny", "Zoe", "Ginger", "Ruby", "Rosie", "Lilly", "Ellie", "Mia", "Sasha", "Lulu", "Pepper", "Nala", "Lexi", "Lady", "Emma", "Riley", "Dixie", "Annie", "Maddie", "Piper", "Princess", "Izzy", "Maya", "Olive", "Cookie", "Roxie", "Angel", "Belle", "Layla", "Missy", "Cali", "Honey", "Millie", "Harley", "Marley", "Holly", "Kona", "Shelby", "Jasmine", "Ella", "Charlie", "Minnie", "Willow", "Phoebe", "Callie", "Scout", "Katie", "Dakota", "Sugar", "Sandy", "Josie", "Macy", "Trixie", "Winnie", "Peanut", "Mimi", "Hazel", "Mocha", "Cleo", "Hannah", "Athena", "Lacey", "Sassy", "Lucky", "Bonnie", "Allie", "Brandy", "Sydney", "Casey", "Gigi", "Baby", "Madison", "Heidi", "Sally", "Shadow", "Cocoa", "Pebbles", "Misty", "Nikki", "Lexie", "Grace", "Sierra"]
    export default {
        data() {
            return {
                image: null,
                gender: genders[Math.floor(Math.random() * genders.length)],
                name: this.gender == 'Pes' ? maleNames[Math.floor(Math.random() * maleNames.length)] : femaleNames[Math.floor(Math.random() * femaleNames.length)],
                region: regions[Math.floor(Math.random() * regions.length)],
                age: Math.floor(Math.random() * (15 - 1) + 1),
                age_suffix: ''
            }
        },
        async mounted() {
            let res = await fetch('https://dog.ceo/api/breeds/image/random')
            let image = await res.json()
            this.image = image['message']

            if(this.age == 1)
                this.age_suffix = 'rok'
            else if(this.age < 5)
                this.age_suffix = 'roky'
            else
                this.age_suffix = 'rokov'
        }
    }
</script>

<template>
    <div style="border: 1px solid rgb(233, 231, 231); margin: 10px 0 10px 0; border-radius: 15px;">
        <a href="#/profile" style="text-decoration: none; color: black">
            <div class="row" style="height: 300px">
                <img style="object-fit: cover; height: inherit; border-top-left-radius: 15px; border-top-right-radius: 15px;" v-bind:src="image">
            </div>
            <div class="container">
                <div class="row" >
                    <h3 style="text-align: center;">{{this.name}}</h3>
                    <p>Pohlavie: {{this.gender}}, Vek: {{this.age}} {{this.age_suffix}}<br>
                    Kraj: {{this.region}}
                    </p>
                </div>
            </div>
        </a>
    </div>
</template>