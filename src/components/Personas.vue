<template>

  <section class="src-components-personas">
    <div class="jumbotron">
      <h2>Personas</h2>

      <button class="btn btn-success my-3 ml-3" @click="getUsuariosThenCatch()">Axio then/catch</button>
      <button class="btn btn-success my-3 ml-3" @click="getUsuariosAsyncAwait()">Axio async/await</button>
      <button class="btn btn-danger my-3" @click="personas = []">CLEAR</button>

      <div v-if="personas.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(persona, index) in personas" :key="index">
            <td>{{persona.nombre}}</td>
            <td>{{persona.edad}}</td>
            <td>{{persona.email}}</td>
          </tr>
        </table>
      </div>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-personas',
    props: [],
    mounted () {

    },
    data () {
      return {
        url: 'https://62b279fd20cad3685c8e74df.mockapi.io/personas',
        personas: [],
      }
    },
    methods: {
      getUsuariosThenCatch(){
        this.axios(this.url)
        .then(({data}) => {
          this.personas = data
          console.log(this.personas);
        })
        .catch(error => console.error('Error Axios', error))
      },
      async getUsuariosAsyncAwait(){
        try {
          let {data} = await this.axios(this.url)
          this.personas = data
          console.log(this.personas);
        } catch (error) {
          console.log("Error Axios", error);        
        }
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-personas {

  }
</style>
