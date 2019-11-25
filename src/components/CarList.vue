<template>
    <div>
        <ul v-for='car of cars' :key="car.id">
            <li>{{ car.name }}</li>
            <li>{{ car.model }}</li>
            <li>{{ car.year }}</li>
        </ul>
        <button @click='addCar'>Add car</button>
        <p>Nombre de voitures : {{ counter }}</p>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "Cars",
        data() {
            return {
                cars: []
            }
        },
        methods: {
            addCar() {
                this.cars.push({
                    'name': 'ford',
                    'model': 'fiesta',
                    'year': '2008'
                })
            }

        },
        computed: {
            counter() {
                return this.cars.length
            }
        },
        mounted() {
            axios
                .get('http://localhost:3000/cars')
                .then(response => { this.cars = response.data })
                .catch(error => {this.errors.push(error)})
        }
    }
</script>

<style scoped>
ul{
    list-style: none;
}
</style>
