

<template>
  <div>
    <h1>Ingresar a la App</h1>
    
    <div class="container">
      
        <form class="caja">
          <input class="form-control mt-3" type="text" placeholder="user" v-model="user" v-on:keyup.enter="loguear">
          <input class="form-control mt-3" type="password" placeholder="password" v-model="pass" v-on:keyup.enter="loguear">
          <button type="submit" @click="loguear" class="btn btn-success mt-4" to="/about" >Login</button>
           <small class="mt-4">User: usuario | Password: 123456</small>
        </form>

     </div>
   
  </div>
</template>



<script>
export default {
  name: 'HelloWorld',
     data () {
      return {
        sesion: [{"user":"usuario","pass":"123456"}],
        user: '',
        pass: ''
      }
  },
  mounted() {
     this.sesion.push({"user":"usuario","pass":"123456"})
      localStorage.setItem('sesion-vue', JSON.stringify(this.sesion));
  },
    methods: {
        loguear: function () {
            let loged =   JSON.parse(localStorage.getItem('sesion-vue'));
        console.log(loged)
        
        if (loged[0].user === this.user && loged[0].pass === this.pass ) {
             this.$router.push('/about');
              this.sesion = [];
        } else {
            this.$router.push('/');
        }
            
        }
        
    }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .caja {
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
    width: 60%;
  }

</style>
