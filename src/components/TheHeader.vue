<template>
    <nav>
        <div class="main">
            <div class="container">
                <h1>TODO</h1>
                <i class="fas fa-sun" @click="$emit('toggle')" v-if=" mode === 'dark'"></i>
                <i class="fas fa-moon" @click="$emit('toggle')" v-else></i>
            </div>
        </div>
    </nav>
</template>
<script>
export default{
    props:['mode'],
}    

</script>

<style scoped>
nav{
    background-image:url('https://images.unsplash.com/photo-1477346611705-65d1883cee1e?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80');
    background-repeat: no-repeat;
    background-size: cover;
    min-height: 35vh;
    width: 100%;
    transition: background 0.3s ease-in-out;
}

.main{
    color: #FFFFFF;
    width: 100%;
    align-items: center;
    margin: 0 auto;
}
.container{
    display: flex;
    justify-content: space-between;
    margin: 0 auto;
    text-align: center;
    width: 80%;
}
h1, i{
    margin-top: 5rem;
}
h1{
    letter-spacing: 12px;
}
/* MEDIA QUERIES  */

@media screen and (min-width: 880px){
    nav{
        background-position: 0 -120px;
    }
    .container{
        width: 60%;
    }
}

/* Light mode  */
.light nav{
    background-image:url('https://images.unsplash.com/photo-1549023068-814b7ead65b5?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1489&q=80');
    background-repeat: no-repeat;
    background-size: cover;
    height: 35vh;
    width: 100%;
}
</style>

