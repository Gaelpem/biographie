<template>
    <div class="container">
        <h1 class="titre">{{ title }}</h1>
        
        <div class="container-image">
            <div class="item">
                <img :src=" './img/1.jpg'"  alt="image">
            </div>
           
            <div class="item">
                <img :src=" './img/2.webp'"  alt="image">
            </div>
            <div class="item">
                <img :src=" './img/3.webp'"  alt="image">
            </div>
         
            <div class="item">
                <img :src=" './img/4.jpg'"  alt="image">

            </div>
           
            <div class="item">
                <img :src=" './img/5.jpg'"  alt="image">
         
            </div>
       
            <div class="item">
                <img :src=" './img/6.jpg'"  alt="image">
           
            </div>
        
            <div class="item">
                <img :src=" './img/7.jpg'"  alt="image">
            </div>
            <div class="item">
                <img :src=" './img/8.jpg'"  alt="image">
            </div>
            <div class="item">
                <img :src=" './img/9.jpg'"  alt="image">
            </div>
            <div class="item">
                <img :src=" './img/10.jpg'"  alt="image">
            </div>
        </div>
    </div>
 
</template>


<script>
export default{
    data(){
        return{
            title :  'Images.'
        }
    }
}
</script>

<style scoped>

.titre{
    font-weight: 600;
    font-size: 4rem;
    font-family: "Josefin Sans", sans-serif;
    color: white;
    max-width: max-content;
}


.container{
    margin-top: 4rem;
    width: 100%;
    display: flex;
    
}

.container-image{
    margin-top: 4rem;
    display: flex;
    flex-wrap: wrap; 
    counter-reset: photocounter;

}
.item{
    border-radius: 7px;
    position: relative;
    display: flex;
    width:  50%;
    margin-bottom: 1rem;
    background-color: rgba(0, 0, 0, 0.28);
    counter-increment: photocounter;
}

.item::after {
  position: absolute;
  content: counter(photocounter,decimal-leading-zero);
  color: rgba(255, 255, 255, 0.397);
  font-size: 2rem;
  right: 0;
  top: 0;
  z-index: 10;
  padding: 1rem;
}

.item img{
    width: 61%;
    height:100%; 
    object-fit: cover;
}

</style>