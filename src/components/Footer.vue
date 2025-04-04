<template>
  <div class="footer">
     <div class="container">
        
          <div class="adress">
            <h3 class="titre1">{{ sign }}</h3>
             <label for="">Adresse email :</label>
             <input type="email" v-model="email">
          </div>


          <div class="resaux">
            <p>Instagram</p>
            <p>Linked in</p>
            <p>Twitter</p>
          </div>
        

           <div class="year">
            <p>©2025</p>
            <p>Développé par GAEL PEMBELE</p>
           </div>
          


     
     </div>
     <div class="big">  
          <h1 class="titre">biography</h1>
        </div>
  </div>
</template>

<script>
export default{
    name:'Footer', 
    data(){
        return{
            sign : "Sign up if you want to join me."
        }
    }

}
</script>


<style scoped>

  .footer{
    margin-top: 5rem; 
    max-height: 100vh;
  }
.container{
    display: flex;
    justify-content: space-between;
    
}
  .titre1{
    color:white; 
    font-weight: 300;
  }



  .adress {
  display: flex;
  flex-direction: column;
  width: 100%; /* Prend toute la largeur */
  max-width: 500px; /* Mais se limite à 500px */
}

label {
  color: white;
  margin: 1.5rem 0 0.5rem 0; /* Marge top/bottom */
  font-size: 0.9rem;
}

input {
  background: transparent;
  border: none;
  border-bottom: 1px solid white;
  width: 100%;
  padding: 8px 0;
  color: white;
  margin-bottom: 1.5rem;
}
p{
    color: white;
}

.big{
    width: 100%;
    overflow: hidden;
    margin: 0 auto;
    height: 220px;
}

.big h1{
    color: white;
    text-transform: uppercase;
    font-size: 17rem;
    font-family: "Josefin Sans", sans-serif;
}
</style>