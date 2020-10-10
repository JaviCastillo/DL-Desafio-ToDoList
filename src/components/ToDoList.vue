<template>
  <div>
    <header>
            <h1>Crea una Lista de Tareas Pendientes (To Do List)</h1>
            <form @submit.prevent="agregarTarea">
                <h2 for="tarea">Ingresa una nueva tarea: </h2>
                <input type="text" v-model="tarea" id="campo">
                <button type="submit">CREAR</button>
                <button @click.prevent="reset">RESET</button>
            </form>
        </header>
        <div v-if="pendientes.length > 0" class="pendientes">
            <h2>Tareas pendientes</h2>
            <ul>
                <li v-for="(valores,index) in pendientes" :key="index">
                    {{index}}: {{ valores }} 
                    <button @click="cumplirTarea(index)">Completar</button>
                    <button @click="borrarTarea(index)">Borrar</button>
                </li>
            </ul>
        </div>
        <div v-if="listas.length > 0" class="listas">
            <h2>Tareas cumplidas</h2>
            <ul>
                <li v-for="(valores,index) in listas" :key="index">
                    {{index}}: {{ valores }} 
                </li>
            </ul>
        </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',
  data(){
    return {
        pendientes: [],
        listas:[],
        tarea: ''
    }
  },
    methods: {
        agregarTarea: function(){
          let resultado = this.pendientes.find(res => res == this.tarea);
          if(this.tarea && !resultado){
              this.pendientes.push(this.tarea);
              this.tarea = '';
          }else{
            alert(`Tarea "${this.tarea}" no valida o ya está agregada`);
          }
        },
        cumplirTarea: function(i){
            let confirmado = confirm(`¿Ha cumplido "${this.pendientes[i]}"?`);
            if(confirmado){
                alert(`Tarea "${this.pendientes[i]}" completada`);
                this.listas.push(this.pendientes[i]);
                this.pendientes.splice(i, 1);
            }

        },
        borrarTarea: function(i){
            let confirmado = confirm(`¿Desea eliminar "${this.pendientes[i]}" de la lista?`);
            if(confirmado){
                alert(`Tarea "${this.pendientes[i]}" eliminada`);
                this.pendientes.splice(i, 1);
            }
        },
        reset: function() {
            this.pendientes = [];
            this.listas = [];
            this.tarea = '';
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  header {
    text-align: center;  
  }
  h1{
      font-size: 60px;
  }
  h2{
      font-size: 40px;
      font-weight: lighter;
  }
  input{
      font-size: 15px;
  }
  form button{
      width: 100px;
      font-size: 15px;
      font-weight: bold;
      margin: 10px;
  }
  .pendientes{
      float: left;
      margin-left: 250px;
  }
  .listas{
      float: right;
      margin-right: 350px;
  }
  ul{
    text-align: left;
  }
  li{
      font-size: 20px;
      line-height: 40px;
  }
  li button{
    margin-left: 10px;
  }
</style>
