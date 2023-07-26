<template>
    <div class="message-container">
        <p>
            {{ msg }}
        </p>
    </div>
</template>

<script>
export default {
    name: "Mensagem",
    props: ["msg"]
}
</script>

<style scoped>
.message-container {
    color: #004086;
    background-color: aliceblue;
    border: 2px solid #88DAFF;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>
