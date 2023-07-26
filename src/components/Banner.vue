<template>
    <div id="main-banner">
        <h1>
            Make your burger
        </h1>
    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style scoped>
#main-banner {
    background-image: url('/public/img/burger.jpg');
    background-position: 0 -250px;
    background-size: cover;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    box-shadow: -10px 10px 9px 4px black;
}

#main-banner h1 {
    color: #fcba03;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
    text-shadow: 5px 5px 5px black;
    box-shadow: 4px 4px 11px 7px black;
}
</style>
