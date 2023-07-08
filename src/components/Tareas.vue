<template>
  <div>
    <h1>#todo</h1>
    <nav class="bar-nav">
      <ul>
        <a class="all" id="all" @click="filtro = 'all'" :style="{  borderBottom: lineaAzulFiltro.all ? '4px solid blue' : 'none' }" >All</a>
        <a class="active" id="active" @click="filtro = 'active'" :style="{ borderBottom: lineaAzulFiltro.active ? '4px solid blue' : 'none'}">Active</a>
        <a class="completed" id="completed" @click="filtro = 'completed'" :style="{ borderBottom: lineaAzulFiltro.completed ? '4px solid blue' : 'none' }" >Completed</a>
      </ul>
    </nav>
    <hr>
    <input type="text" id="textoTarea" class="newtarea" placeholder="add details" v-model="nuevaTarea"/>
    <button type="submit" class="send" @click="crearTarea">Add</button>

    <div id="listaTareas">
      <p v-for="(tarea, index) in tareasFiltradas" :key="index" class="tarea">
        <input type="checkbox" class="check" v-model="tarea.completada">
        <span :style="{ textDecoration: tarea.completada ? 'line-through' : 'none' }">{{ tarea.texto }}</span>
        <button class="borrar" @click="borrarTarea(index)" :style="{ display: mostrarBotones ? 'block' : 'none' }">&#128465;</button>
      </p>
    </div>

    <button type="submit" class="delete" @click="borrarTodasLasTareas" :style="{ display: mostrarBotones ? 'block' : 'none' }">&#128465;Delete all</button>

  </div>
</template>

<script>
export default {
  name: "ListaTareas",
  data() {
    return {
      nuevaTarea: '',
      tareas: [],
      filtro: 'all',
      mostrarBotonoes: false
    };
  },
  methods: {
    crearTarea() {
      if (this.nuevaTarea !== '') {
        this.tareas.push({
          texto: this.nuevaTarea,
          completada: false
        });
        this.nuevaTarea = '';
      }
    },
    borrarTarea(index) {
      this.tareas.splice(index, 1);
    },
    borrarTodasLasTareas() {
      this.tareas = [];
    }
  },
  
  computed: {
  lineaAzulFiltro() {
    const estadoFiltro = {
      active: false,
      completed: false,
      all: false
    };

    if (this.filtro === 'active') {
      estadoFiltro.active = true;
    } else if (this.filtro === 'completed') {
      estadoFiltro.completed = true;
    } else {
      estadoFiltro.all = true;
    }
    return estadoFiltro;
    },
    tareasFiltradas() {
      if (this.filtro === 'active') {
        return this.tareas.filter(tarea => !tarea.completada);
      } else if (this.filtro === 'completed') {
        return this.tareas.filter(tarea => tarea.completada);
      } else {
        return this.tareas;
      }
    }
  },
    
  watch: {
    tareasFiltradas: {
      handler(nuevasTareasFiltradas) {
        this.mostrarBotones = nuevasTareasFiltradas.some(tarea => tarea.completada);
      },
      immediate: true
    }
  } 

};
</script>




<style scoped>
  h1{
    color: #333;
    text-align: center;
    font-size: 36px;
    font-family: Raleway;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
    letter-spacing: -1.62px;
  }
  .all{
    position: absolute;
    top: 130px;
    left: 500px;
  }

  .active{
    position: absolute;
    top: 130px;
    left: 580px;
  }
  
  .completed{
    position: absolute;
    top: 130px;
    left: 700px;
  }

  a{
    color: #333;
    font-size: 16px;
    font-family: Montserrat;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    height: 46px;
    width: 46px;
  }

  .active {
    width: 80px;
  }

  .completed {
    width: 100px;
  }

  ul{
    list-style:none;
  } 

  hr{
    width: 700px;
    position: absolute;
    top: 170px;
    left: 300px;
  }

  .newtarea{
    width: 420px;
    height: 56px;
    flex-shrink: 0;
    border-radius: 12px;
    border: 1px solid #BDBDBD;

    position: absolute;
    top:200px;
    left: 350px;
    padding-left: 20px;
  }

  ::placeholder{
    font-size: 14px;
    font-family: Montserrat;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
  }

  .send{
    color: white;
    border-radius: 12px;
    background: #2F80ED;
    box-shadow: 0px 2px 6px 0px rgba(127, 177, 243, 0.40);
    width: 109px;
    height: 56px;
    flex-shrink: 0;
    border: none;

    position: absolute;
    top:200px;
    left: 850px;
  }
  
  a:hover{
    cursor: pointer;
  }


  .delete{
    width: 124px;
    height: 40px;
    flex-shrink: 0;
    border-radius: 4px;
    background: #EB5757;
    border: none;
    color: white;

    position: absolute;
    top: 500px;
    left: 850px;
  }

  #listaTareas{
    position: absolute;
    top: 270px;
    left: 350px;
    width: 400px;
    height: 40vh;
    padding: 20px;
    text-align: left;
  }

  .delete:hover{
    cursor: pointer;
    scale: 1.05;
  }

  .send:hover{
    cursor: pointer;
    scale: 1.05;
  }
  
  .delete:active{
    background: #dd4c4c;
    scale: 0.95;
  }

  .send:active{
    background: #205eaf; 
    scale: 0.95;
  }

  .borrar{
    position: absolute;
    left: 400px;
    border: none;
    background: white;
    scale: 1.4;
  }

  .borrar:hover{
    cursor: pointer;
  }
  .borrar:active{
    background: silver;
    border-radius: 10px;
    scale: 1.2;
  }

  .all, .active, .completed {
    text-decoration: outlined;
  }
  
</style>




