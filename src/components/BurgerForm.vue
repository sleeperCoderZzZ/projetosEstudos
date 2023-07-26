<template>
    <div>
        <Mensagem :msg="msg" v-if="msg" />
        <div id="burger-form-geral">
            <form id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label id="opcionais-tittle" for="nome">nome do cliente</label>
                    <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">escolha o seu pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">escolha o seu carne:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">selecione o seu carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>
                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-tittle" for="opcionais">escolha o seu opcional:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisData" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                    <div class="submit-btn">
                        <input type="submit" value="Finalize o seu pedido!">

                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Mensagem from "./Mensagem.vue";

export default {
    name: "BurgerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisData: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: ""
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisData = data.opcionais;
        },
        async createBurger(e) {

            e.preventDefault();

            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "content-type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} realizado com sucesso`


            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";

        }
    },
    mounted() {
        this.getIngredientes()
    },
    components: {
        Mensagem
    }
}
</script>

<style scoped>
#burger-form-geral {
    display: flex;
    flex-direction: column;
    align-items: center
}

#burger-form {
    max-width: 350px;
    margin: 0 auto;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;


}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222233;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-tittle {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
    background-color: #201f1f;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>


