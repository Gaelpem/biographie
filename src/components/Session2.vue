<template>
  <div class="session1">
    <h1>{{ titre1 }}</h1>
    <p>{{ description }}</p>
    <div class="decoration">

    </div>
  </div>
</template>

<script>
export default{
    name : 'Session1',
    data(){
        return{
            titre1 : "Biographie.",
            description:'Henri Cartier-Bresson (1908-2004) est l’un des photographes les plus influents du XXe siècle, considéré comme un pionnier du photojournalisme et de la photographie de rue. Né à Chanteloup-en-Brie, en France, il se passionne très tôt pour l’art et découvre la photographie après avoir été influencé par le surréalisme.'
        }
    }
}
</script>


<style scoped>

.session1{
 max-width: 95%;
 margin: 0 auto;
 display: flex;


}

h1{
    border-top: 0.5px solid white;
 width: 65%;
    color: white;
  font-family: "Imbue", serif;
  font-weight: 200;
  font-size: 8rem;
}

p{
    color: white;
    font-size: clamp(1.1rem, 4vw, 2rem);
    width: 40%;
    font-weight: 300;
    font-family:"Inter", sans-serif;
    font-weight: 200; 
    text-align: justify;


}
.decoration{
border-top: 0.5px solid white;
 width: 15%;
}
</style>