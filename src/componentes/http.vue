
<template>


  <section class="src-componentes-http">
    <div class="jumbotron">
        <h2>Usuarios</h2>
        <hr>
        <button class="btn btn-warning my-3 mr-3" @click="getPostsAxios()" >Then&Catch</button>
        <button class="btn btn-success my-3" @click="getPostsAxiosAsync()" >AsyncAwait</button>


        <div v-if="posts.length" class="table-responsive">
          <table class="table table-dark">
            <!-- encabezado de la tabla -->
            <tr>
              <th v-for="(col,index) in getCols" :key="index">{{col}}</th>
            </tr>

            <!-- filas con los datos -->
            <tr v-for="(post,index) in posts" :key="index">

              <td v-for="(col,index) in getCols" :key="index">{{post[col]}}</td>
            </tr>
          </table>
          <h4 class="alert alert-primary">Se encontraron {{posts.length}} posts.</h4>
        </div>
        <h4 v-else class="alert alert-warning">No se encontraron posts</h4>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-http',
    props: [],
    mounted () {
      this.getPostsAxios();
    },

    data () {
      return {

        url : 'https://60c13689b8d3670017556a6d.mockapi.io/usuario/user',
        posts : []
      }
    },
    methods: {

      getPostsAxios() {
        this.axios(this.url)
        .then( respuesta => {
          console.log('AXIOS',respuesta.data)
          this.posts = respuesta.data
        })
        .catch(error => console.log(error))
      },
      async getPostsAxiosAsync() {
          try {
              const resp = await this.axios.get(this.url);
              this.posts = resp.data
              console.log(resp.data);
          } catch (err) {
              console.error(err);
            }
      },
    },
    computed: {
      getCols() {
        return Object.keys(this.posts[0])
      }
    }
}

</script>

<style scoped lang="css">
 .src-componentes-http {
      color: #333;
  }

.container {
   
    background: rgb(233, 151, 0); /* Old browsers */
    display: flex;
    justify-content: space-around;
    padding-top: 20px;
    color: rgb(253, 0, 0);
  }

  hr {
    background-color: rgb(251, 255, 0);
  }  
</style>
