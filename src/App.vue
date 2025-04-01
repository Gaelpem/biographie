
<template>

  <header>
    <Navbar/>
  </header>

  <main>

    <div class="presentation">
      <img :src="'/cartier1.webp'" alt="image">
      <h1>{{ titre1 }}</h1>
    </div>



<Session2/>
<Session3/>
  </main>

</template>


<script >
import Navbar from './components/Navbar.vue';
import Session2 from './components/Session2.vue';
import Session3 from './components/Session3.vue';


export default{
  name: 'App',
  components:{
    Navbar,
    Session2,
    Session3
},
  data(){
    return{
      titre1 : "Henri Cartier-Bresson."
    }
  }
}
</script>

<style scoped>

main{
min-height: 55vh;
margin-top: 2rem;
margin: 0 auto;
padding: 1rem;

}

.presentation{
  max-width: 95%;
  margin: 0 auto;
}
img{
  width: 100%;
  height: 690px; /* Hauteur fixe pour le crop */
  object-fit: cover; /* Recadre l'image */
  object-position: bottom; /* Aligne le crop en haut */
}
h1{
  color: white;
  font-family: "Imbue", serif;
  font-weight: 200;
  font-size: 8rem;

}
</style>
