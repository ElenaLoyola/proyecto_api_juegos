<template>
    <div id="Administracion">
        <div v-if="flagButton">
            <h3 id="titulo">Para ver la información ingresa tus datos</h3>
            <button class="btn btn-success" v-on:click="mostrarFormulario">Ingresar Datos</button>
        </div>
        <div id="divForm" v-if="flagForm" class="container">
            <form>
                <div class="mb-3">
                    <label for="txtNombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviado" aria-describedby="txtNombreHelp">
                </div>
                <div class="mb-3">
                    <label for="txtApellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="txtApellido" v-model="apellidoEnviado">
                </div>
                <button type="submit" v-on:click.prevent="enviarDatos()" class="btn btn-info">Enviar</button>
            </form>
        </div>
        <div v-if="flagResumen" class="container">
            <div class="row">
                <div id="seccionNombre" class="col-md-3">
                    <img src="@/assets/user.png" alt="imagen usuario">
                    <p>Bienvenid@</p>
                    <p>{{ nombreEnviado }} {{ apellidoEnviado }}</p>
                </div>
                <div class="col-md-9">
                    <div class="container">
                        <div class="row">
                            <div class="col-md-12">
                                <h2>Resumen de tu cuenta</h2>
                                <h4>Le diste me gusta al juego: <b>{{ nombre }}</b></h4>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <div id="divCoins" class="container text-center">
                                    <p>¿Deseas comprar coins para este juego?</p>
                                    <button id="btnCoins" class="btn btn-warning" v-on:click="agregarCoins"><i class="fa-solid fa-coins" style="color: #000000;"></i>Agregar Coins</button>
                                    <hr>
                                    <h4>Cantidad de Coins Comprados</h4>
                                    <div class="progress" role="progressbar" aria-label="Example with label" v-bind:aria-valuenow="cantidadCoins" aria-valuemin="0" aria-valuemax="100">
                                        <div class="progress-bar bg-success" style="">${{cantidadCoins}}</div>
                                    </div>
                                    <div v-if="flagMaximo">
                                        <p class="text-danger">Llegaste al maximo de tu credito</p>
                                    </div>
                                    <br><br>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-4 bg-warning resumen">
                                <p>% de finalización de juego</p>
                                <hr>
                                <p>17% <i class="fa-solid fa-star-half"></i></p>
                            </div>
                            <div id="pColor"  class="col-md-4 bg-success resumen">
                                <p>Logros en el juego </p>
                                <hr>
                                <p>66 <i class="fa-solid fa-trophy" style="color: #ffffff;"></i></p>
                            </div>
                            <div class="col-md-4 bg-info resumen">
                                <p >Recompensas</p>
                                <hr>
                                <p>200 <i class="fa-solid fa-award"></i></p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <p id="volverHome"><router-link to="/">Volver</router-link></p>
    </div>
</template>

<script>
export default{
    name:'Administracion',
    props:['nombre'],
    data: function(){
        return{
            flagButton:true,
            flagForm:false,
            flagResumen:false,
            flagMaximo:false,
            nombreEnviado:'',
            apellidoEnviado:'',
            cantidadCoins:0,
        }
    },
    methods:{
        mostrarFormulario:function(){
            this.flagButton = false;
            this.flagForm = true;
        },
        enviarDatos:function(){
            this.flagForm = false;
            this.flagResumen = true;
        },
        agregarCoins:function() {
            this.cantidadCoins++;
            let laBarra = document.getElementsByClassName('progress-bar');
            let valorPorCiento='';
            if(this.cantidadCoins < 50){
                valorPorCiento = `${this.cantidadCoins}%`;
                laBarra[0].style.width =valorPorCiento;
                if(this.cantidadCoins > 20 && this.cantidadCoins <= 30){
                    laBarra[0].classList.remove('bg-success');
                    laBarra[0].classList.add('bg-warning');
                }
                else if(this.cantidadCoins > 30){
                    laBarra[0].classList.remove('bg-warning');
                    laBarra[0].classList.add('bg-danger');
                }
            }else{
                this.flagMaximo = true;
                let elBotonCoins = document.getElementById('btnCoins');
                elBotonCoins.setAttribute('disabled', true);
            }
        },
    }
}
</script>

<style scoped>
#Administracion{
    background-color: rgb(255, 255, 255);
    width: 70%;
    margin: 0 auto;
}
#titulo {
    margin-top: 20px;
    margin-bottom: 40px;
}
#seccionNombre{
    background-color: black;
    color:white;
}
#divCoins{
    background-color: rgb(255, 255, 255);
    border: 1px solid gray;
    border-radius: 5px;
    margin-bottom: 30px;
}
#divCoins p {
    margin-top: 15px;
}
#volverHome {
    margin: 20px;
}
a {
    text-decoration: none;
}
#divForm{
    background-color: rgb(255, 255, 255);
    text-align:start;
    width: 80%;
    margin: 0 auto;
    margin-top: 20px;
}
form label {
    font-weight: bold;
}
img {
    width: 30%;
    margin-top: 20px;
    margin-bottom: 10px;
}
h2 {
    margin-top: 20px;
    margin-bottom: 40px;
}
h4 {
    margin-bottom: 20px;
    color: #2c3e50;
}
.resumen p {
    font-size: 20px;
    margin-top: 10px;
}
#pColor p {
    color: white;
}
</style>