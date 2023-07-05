<template>
    <div id="OpinionesView">
        <h3>Escribe tu opinión para el juego: {{ nombre }}</h3>
        <div class="container" id="divForm">
            <form>
                <div class="mb-3">
                    <label for="txtNombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviado" aria-describedby="txtNombreHelp">
                </div>
                <div class="mb-3">
                    <label for="txtOpinion" class="form-label">Opinión:</label>
                    <textarea  class="form-control" v-model="opinionEnviada" name="txtOpinion" id="txtOpinion" cols="30" rows="4" placeholder="Tu opinión debe ir aquí..."></textarea>
                </div>
                <button type="submit" v-on:click.prevent="agregarOpinion()" class="btn btn-info">{{nombreBoton}}</button>
            </form>
        </div>
        <h3>A continuación podrás ver tu opinión</h3>
        <div id="sinOpiniones" v-if="cantidadOpiniones < 1">
            <p>No existen opiniones para mostrar</p>
        </div>
        <div class="accordion" id="accordionExample" v-if="cantidadOpiniones > 0">
            <div class="accordion-item" v-for="(elemento,index) in opiniones">
                <h2 class="accordion-header">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                    Opinion creada por: {{ elemento.nombre }}
                </button>
                </h2>
                <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
                    <div class="accordion-body">
                        {{ elemento.opinion }}
                    </div>
                    <button class="btn btn-danger m-2" v-on:click="eliminarOpinion(index)">Eliminar</button>
                    <button class="btn btn-warning m-2" v-on:click="editarOpinion(index)">Editar</button>
                </div>
            </div>
        </div>
        <p id="volverHome"><router-link to="/">Volver</router-link></p>
    </div>
</template>

<script>
export default{
    name:'OpinionesView',
    props:['nombre'],
    data: function(){
        return{
            cantidadOpiniones: 0,
            nombreEnviado:'',
            opinionEnviada:'',
            opiniones:[],
            nombreBoton:'Agregar',
            indiceActualizar:0,
        }
    },
    methods:{
        agregarOpinion: function(){
            if(this.nombreBoton == 'Agregar'){
                this.cantidadOpiniones++;
                let nuevaOpinion = {
                nombre:this.nombreEnviado,
                opinion:this.opinionEnviada,
                };
                this.opiniones.push(nuevaOpinion);
                this.nombreEnviado='';
                this.opinionEnviada='';
            }
            else if(this.nombreBoton=='Actualizar'){
                let opinionActualizada = {
                    nombre:this.nombreEnviado,
                    opinion:this.opinionEnviada,
                };
                this.opiniones.splice(this.indiceActualizar,1, opinionActualizada);
                alert('La opinión fue actualizada. Revise el acordeon con la nueva inforación');
            }
        },
        eliminarOpinion:function(indice){
            this.cantidadOpiniones--;
            this.opiniones.splice(indice,1);
        },
        editarOpinion:function(indice){
            this.nombreEnviado=this.opiniones[indice].nombre;
            this.opinionEnviada=this.opiniones[indice].opinion;
            this.nombreBoton = 'Actualizar';
            this.indiceActualizar = indice;
            alert('Va a editar una opinión. Revise el formulario con la información cargada');
        },
    }
}
</script>

<style scoped>
#OpinionesView{
    background-color: rgb(255, 255, 255);
}
h3 {
    margin-top: 20px;
    margin-bottom: 40px;
}
#divForm{
    background-color: rgb(255, 255, 255);
    text-align:start;
    width: 70%;
    margin: 0 auto;
}
form label {
    font-weight: bold;
}
#sinOpiniones {
    border: 2px solid rgb(255, 136, 136);
    background-color: rgb(245, 175, 175);
    color: brown;
    width: 70%;
    margin: 0 auto;
    padding: 1%;
    border-radius: 5px;
}
#sinOpiniones p {
    margin-bottom: 0px;
}
#volverHome {
    margin: 20px;
}
a {
    text-decoration: none;
}
#accordionExample {
    width: 70%;
    margin: 0 auto;
}
#collapseOne {
    text-align: start;
}
</style>