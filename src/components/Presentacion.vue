<template>
    <div>
        <div v-if="!showCard">
            <button @click="solicitarDatos" class="btn btn-success">Ingresar Datos</button>
        </div>
        <div class="card-style" v-if="showCard">
            <div class="card text-center">
                <div class="card-header"></div>
                    <div class="card-body">
                        <h5 class="card-title">¡Bienvenid@ {{fullName}}!</h5>
                        <p class="card-text">Aquí podrás encontrar información de películas de Studio Ghibli</p>
                        <button class="btn btn-danger" @click="limpiarWeb">Limpiar Información</button>
                    </div>
                <div class="card-footer text-body-secondary"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'presentacion-view',
    props: {
        showCard: {
            type: Boolean,
            default: false,
        },
    },
    data() {
        return {
            name: '',
            lastName: '',
        };
    },
    methods: {
        solicitarDatos() {
            this.name = prompt('Ingrese su nombre:');
            this.lastName = prompt('Ingrese su apellido:');
            this.$emit('toggleCard', true);
        },
        limpiarWeb() {
            this.name = '';
            this.lastName = '';
            this.$emit('toggleCard', false);
        },
    },
    computed: {
        fullName() {
            return this.name + ' ' + this.lastName;
        },
    },
};
</script>

<style scoped>
.card-style {
    display: flex;
    justify-content: center;
}

.card {
    width: 40%;
    margin-top: 20px;
    box-shadow: rgba(255, 0, 255, 0.35) 0px 5px 15px;
}

</style>
