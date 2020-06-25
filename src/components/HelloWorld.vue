<template>
  <div>
    <b-row class="mt-5 justify-content-sm-center">
      <b-col sm="12" md="8" lg="6">
        <h1 class="text-center">{{titulo}}</h1>
        <b-row>
          <b-col cols="12">
            <b-form-input 
              v-model="nuevaTarea"
              placeholder="Ingresa rutina"
              class="my-3"
              @keyup.enter="agregarTarea"
            ></b-form-input>
          </b-col>
          <b-col cols="12">
            <b-button variant="info" @click="agregarTarea">Agregar</b-button>
          </b-col>
          <b-col cols="12" class="mt-5">
            <b-alert 
              show 
              v-for="(tarea, index) of tareas"
              :key="tarea.id"
              :variant="tarea.estado ? 'success' : 'danger'"
            >
              <div class="d-flex justify-content-between align-items-center">
                <div>{{index+1}} - {{tarea.nombre}} - <strong>{{tarea.estado}}</strong></div>
                <div>
                  <b-button variant="success" size="sm" @click="editarTarea(index)">
                    <b-icon icon="check-circle-fill"></b-icon>
                  </b-button>
                  <b-button variant="danger" class="ml-1" size="sm" @click="eliminar(index)">
                    <b-icon icon="trash-fill"></b-icon>
                  </b-button>
                </div>
              </div>
            </b-alert>
          </b-col>
        </b-row>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return {
      titulo: "Gym con Vue",
      nuevaTarea: "",
      tareas: []
    }
  },
  methods: {
    agregarTarea(){
      this.tareas.push({
        nombre: this.nuevaTarea,
        estado: false
      });
      localStorage.setItem('vue-gym', JSON.stringify(this.tareas));
      this.nuevaTarea = "";
    },
    editarTarea(index){
      this.tareas[index].estado = !this.tareas[index].estado;
      localStorage.setItem('vue-gym', JSON.stringify(this.tareas));
    },
    eliminar(index){
      this.tareas.splice(index, 1);
      localStorage.setItem('vue-gym', JSON.stringify(this.tareas));
    }
  },
  created(){
    let datosLS = JSON.parse(localStorage.getItem('vue-gym'));
    console.log(datosLS);
    if (datosLS === null) {
      this.tareas = [];
    } else {
      this.tareas = datosLS;
    }
  }
}
</script>
