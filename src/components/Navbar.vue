<template>
    <nav>
        <ul>
            <li><a href="#">index</a></li>  
            <li><a href="#">biographie</a></li>
            <li><a href="#">photographie</a></li>
        </ul>
    </nav>

</template>

<script>
export default{
    name : 'Navbar',
}
</script>

<style scoped>


nav{
  width: 100%;
  max-width: 1500px;
  padding: 1rem;
}
nav ul{
    display: flex;
    justify-content: space-between;
}
li{
    list-style: none;
}
li a{
    text-decoration: none;
    color: white;
    font-size: 1.2rem;
    font-family:Arial, Helvetica, sans-serif
}
</style>