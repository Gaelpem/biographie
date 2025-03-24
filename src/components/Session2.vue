<template>
  <div class="session1">
    <h1>{{ titre1 }}</h1>
  </div>
</template>

<script>
export default{
    name : 'Session1',
    data(){
        return{
            titre1 : "Biographie",
        }
    }
}
</script>


<style scoped>

.session1{
 border-top: 0.5px solid white;
}

h1{
    color: white;
  font-family: "Imbue", serif;
  font-weight: 200;
  font-size: 8rem;
}
</style>