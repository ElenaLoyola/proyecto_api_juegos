<template>
    <div id="Juegos">
        <div class="contenedorPadre">
            <div v-for="(juego,index) in juegos" v-bind:key="index" id="caja" class="card mb-5" style="width: 18rem;">
                <img v-bind:src="juego.background_image" class="card-img-top" alt="logo">
                <div class="card-body">
                    <h5 class="card-title">{{ juego.name }}</h5>
                    <p class="card-text">ESRB Rating: {{  juego.esrb_rating.name }}</p>
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Rating: {{ juego.rating }}</li>
                    <li class="list-group-item">Released: {{  juego.released }}</li>
                    <li class="list-group-item">Updated: {{  juego.updated }}</li>
                </ul>
                <div class="card-body">
                    <a v-on:click="mostrarOpiniones(juego.name)" class="btn btn-primary">Opinar</a>
                    <a v-on:click="irAdministracion(juego.name)"><i class="fa-solid fa-heart fa-xl" style="color: #ff0000;"></i></a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default{
    name:'Juegos',
    data:function(){
        return{
            cantidadJuegos:0,
            juegos:[],
        }
    },
    methods:{
        consumirApi:function(){
            let url='https://api.rawg.io/api/games?key=2bac88791855496f969cf9ad978d9922';
            axios(url)
            .then(respuesta =>{
                this.cantidadJuegos = respuesta.data.results.length;
                for(let i=0; i < this.cantidadJuegos; i++){
                    this.juegos.push(respuesta.data.results[i]);
                }
            })
            .catch(error=>{
                console.log(error);
            });
        },
        mostrarOpiniones:function(nombreJuego){
            this.$router.push(`/opiniones/${nombreJuego}`);
        },
        irAdministracion:function(nombreJuego){
            this.$router.push(`/administracion/${nombreJuego}`);
        },
    },
    created(){
        this.consumirApi();
    }
}
</script>

<style scoped>
#Juegos{
    background-color: rgb(255, 255, 255);
    margin: 0 auto;
}

.contenedorPadre{
    display:flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 80%;
    margin: 0 auto;
}
img {
    height: 145px;
}
i {
    cursor: pointer;
    margin-left: 10px;
}
i:hover {
    animation: beat .35s infinite alternate;
	transform-origin: center;;
}
@keyframes beat{
	to { transform: scale(1.4); }
}
/* Dispositivos extra pequeños (teléfonos, 600px y menos) */
@media only screen and (max-width: 600px) {
    .contenedorPadre{
    justify-content: center;
    width: 90%;
    }
} 
/* Dispositivos pequeños (tablets verticales y teléfonos grandes, 600px y más) */ 
@media only screen and (min-width: 600px) and (max-width: 767px){
    .contenedorPadre{
    justify-content: space-around;
    width: 100%;
    }
}
</style>