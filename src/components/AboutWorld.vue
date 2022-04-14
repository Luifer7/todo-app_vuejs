

<template>

    <!-- App -->
    <div class="container">

      
           <div class="d-flex justify-content-center align-items-center box">
               <h2 class="text-center m-2" mt-3>Tareas-App</h2>
               <input class="m-2 form-control box_search" type="text" placeholder="Buscar tarea" v-model="query" v-on:input="('search', query)">
           </div>
            

            <div class="card mb-2">
                <div class="card-header">
                    <div class="mb-2">
                        
                        <input placeholder="Escriba una Tarea" class="form-control" type="text" required v-model="nuevaTarea" v-on:keyup.enter="agregarNuevaTarea">
                    </div>
                    <div class="mb-2">
                        
                        <input placeholder="Describa la Tarea" class="form-control" type="text" required v-model="nuevaTareaDescripcion" v-on:keyup.enter="agregarNuevaTarea">
                    </div>
                    <div class="mb-2 tg">
                        
                        <input placeholder="Taggs" class="form-control" type="text" required v-model="nuevaTareaTaggs" v-on:keyup.enter="agregarNuevaTarea">
                        <input placeholder="Taggs" class="form-control m-1" type="text" required v-model="nuevaTareaTaggsDos" v-on:keyup.enter="agregarNuevaTarea">
                        <input placeholder="Taggs" class="form-control" type="text" required v-model="nuevaTareaTaggsTres" v-on:keyup.enter="agregarNuevaTarea">
                    </div>
                    <div class="mt-2">
                        <button @click="agregarNuevaTarea" class="btn btn-outline-success">Guardar</button>
                    </div>
                    
                </div>
            
            </div>

           

            <div class="card-body" v-for="(item, index) in tareas" :key="index">

                <div class="row bga_ justify-content-center align-items-center border rounded">

                    <!-- Tarea -->
                    <div class="col">

                        <div class="d-flex justify-content-evenly align-items-center" >
                            <p :class="[item.estado==='Pendiente' ? 'm-3' : 'text-decoration-line-through m-3']">
                                <b>{{item.nombre}}</b>
                            </p>
                            <!-- Button Collapse -->
                            <p class="m-3"><button class="btn_btn_" type="button" data-bs-toggle="collapse" v-bind:data-bs-target="'#'+item.taggs">
                                <svg xmlns="http://www.w3.org/2000/svg" width="23" height="23" fill="currentColor" class="bi bi-three-dots" viewBox="0 0 16 16">
                                <path d="M3 9.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3zm5 0a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3zm5 0a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3z"/>
                                </svg>
                            </button> </p>
                        
                        </div>
                            <!-- collapse -->
                              <div class="collapse mb-2 justify-content-center align-items-center" v-bind:id="item.taggs">
                                   
                                        <small :class="[item.estado==='Pendiente' ? 'descripcion m-3' : 'text-decoration-line-through m-3']">
                                            {{item.descripcion}}
                                        </small>
                                        <small :class="[item.estado==='Pendiente' ? 'taggs_ m-3' : 'text-decoration-line-through m-3']">
                                            <b>#{{item.taggs}}</b> | <b>#{{item.taggsDos}}</b> | <b>#{{item.taggsTres}}</b>
                                        </small>
                              </div>    
                    </div> <!-- Col end -->

                    <!-- Botones -->
                    <div class="col">

                              
                            <!-- Tarea terinada -->
                        <div  class="d-flex bga justify-content-center align-items-center ">

                            <small :class="[item.estado==='Pendiente' ? 'bga____ m-3' : 'bga___']">
                                <b>{{item.estado}}</b>
                            </small>

                            <buttton class="m-3" @click="tareaRealizada(index)">
                                <svg  xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="currentColor" class="bi bi-check-circle green" viewBox="0 0 16 16">
                                <path class="green" d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
                                <path d="M10.97 4.97a.235.235 0 0 0-.02.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-1.071-1.05z"/>
                                </svg>
                            </buttton>

                            <!-- Delete -->
                            <buttton class="m-3  red" @click="eliminar(index)" >
                                <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="currentColor" class="bi bi-trash3 red" viewBox="0 0 16 16">
                                <path class="red" d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z"/>
                                </svg>
                            </buttton>

                        </div>

                    </div>
                        
                        <!-- Strange -->
                        
                      

                </div>
            
    
            </div>
            <div class="mt-3">
             <small class="mt-3">© 2022 By: Luis Fernando Cordero</small>
          </div>

    </div>

</template>


<script>


export default {
  name: 'AboutWorld',
  data () {
      return {
        nombre: "Tareas App",
        tareas: [],
        copyTareas: [],
        nuevaTarea: '',
        nuevaTareaDescripcion: '',
        nuevaTareaTaggs: '',
        nuevaTareaTaggsDos: '',
        nuevaTareaTaggsTres: '',
        query: ''
      }
  },
  mounted(){
      
      if (localStorage.getItem('sesion-vue')) {
          this.$router.push('/about');
      } else {
           this.$router.push('/');
      }
     
  },
  methods: {
       agregarNuevaTarea:  function () {
            this.tareas.push({
                nombre: this.nuevaTarea,
                descripcion: this.nuevaTareaDescripcion,
                taggs: this.nuevaTareaTaggs,
                taggsDos: this.nuevaTareaTaggsDos,
                taggsTres: this.nuevaTareaTaggsTres,
                estado: 'Pendiente' 
            })
             localStorage.setItem('tareas-vue', JSON.stringify(this.tareas));
            console.log(this.tareas);
            this.nuevaTarea = '';
            this.nuevaTareaDescripcion = '';
            this.nuevaTareaTaggs = '';
            this.nuevaTareaTaggsDos = '';
            this.nuevaTareaTaggsTres = '';
       },
        tareaRealizada: function (index) {
            this.tareas[index].estado = "Realizada";
            localStorage.setItem('tareas-vue', JSON.stringify(this.tareas));
        },
         eliminar: function (index) {
            this.tareas.splice(index, 1);
            localStorage.setItem('tareas-vue', JSON.stringify(this.tareas));
        },
        
  },
   created: function () {
       
        let datosLS = JSON.parse(localStorage.getItem('tareas-vue'));
        
        console.log(datosLS)
        if (datosLS === null) {
            this.tareas = [];
             this.copyTareas = [];
        } else {
            this.tareas = datosLS;
             this.copyTareas = datosLS;
           
        }
    }
}


</script>


<style scoped>

.box {
    width: 70%;
    margin: 0 auto;
}

.tg {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 4px;
}
.caja-formulario {
    margin: 0 auto;
    width: 50%;
    height: 250px;
    background: rgb(245, 241, 241);
    
    border-radius: 5px;
    display: flex;
    flex-direction: column;
}

.card {
    width: 90%;
    margin: 0 auto;
}

.bga {
    background: rgb(245, 241, 241);
    height: 50px;
}

.bga_ {
background: rgb(245, 241, 241);

}

.bga___ {
    color: green;
}
.bga____ {
    color: rgb(128, 0, 0);
}

.form-control {
    width: 60%;
    margin: 0 auto;
}

svg {
    cursor: pointer;
}

.green:hover{
    color: green;
}
.red:hover{
    color: rgb(209, 1, 1);
}

.form-control::placeholder{
    text-align: center;
    font-size: .9em;
}

.descripcion {
    color: rgb(146, 136, 136);
    font-size: .8em;
    display: flex;
    align-items: center;
    justify-content: center;
}

.taggs_ {
    color: rgba(11, 11, 95, 0.911);
    font-size: .8em;
    
}

.card-body{
    padding: 5px;
}

.btn_btn_ {
    border: none;
    outline: none;
    color: blue;
}

@media (min-width: 800px) {
    .card {
    width: 60%;
    margin: 0 auto;
} 
}



</style>