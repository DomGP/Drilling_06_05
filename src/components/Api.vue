<template>
    <div>
        <div class="select-style">
            <select v-model="selectedMovie" class="form-select">
                <option value="" selected disabled>Seleccione una película</option>
                <option v-for="(movie,index) in movies" :key="index" :value="movie.name">{{capitalizeFirstLetter(movie.name)}}</option>
            </select>
        </div>
        <div class="card-style" v-if="film != undefined">
            <div class="card" style="width: 18rem;">
                <img :src="film.data.poster" class="card-img-top" alt="...">
                <div class="card-body">
                    <h4 class="card-title">Titulo Original: {{capitalizeFirstLetter(film.data.hepburn)}}</h4>
                    <h5 class="card-title">Titulo Romanizado: {{capitalizeFirstLetter(film.name)}}</h5>
                    <p class="card-text">Descripción: {{capitalizeFirstLetter(film.data.synopsis)}}</p>
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Director: {{film.data.director}}</li>
                    <li class="list-group-item">Duración: {{film.data.runtimeMinutes}} minutos</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'component-name',
    data: function(){
        return {
            movies:[],
            selectedMovie:null,
        }
    },
    methods: {
        axiosMovies(){
            axios.get(`https://studio-ghibli-films-api.herokuapp.com/api`)
            .then(response => {
                for(const property in response.data){
                    let myMovie = {
                        name: property,
                        data: response.data[property]
                    }
                    this.movies.push(myMovie)
                }
                
            })
            .catch(error => {
                console.error(error);
            });
        },
        capitalizeFirstLetter(text) {
            return text.charAt(0).toUpperCase() + text.slice(1);
        },
    },
    computed: {
        film(){
            let movie = this.movies.find(movie=>movie.name==this.selectedMovie)
            return movie

        }
    },
    // props: {},
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    created(){
        this.axiosMovies();
        this.selectedMovie="";
    }
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    .select-style{
        display: flex;
        justify-content: center;

    }
    .form-select{
        margin-top:50px;
        box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
        width: 20%;
    }
    .card-style{
        display: flex;
        justify-content: center;
        margin-top: 20px;
        margin-bottom: 20px;
    }
</style>

