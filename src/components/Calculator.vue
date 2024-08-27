<template>
    <div class="calculator">
        <div class="display">
            <input v-model="input1" type="number" placeholder="Numero 1" />
            <select v-model="operation">
            <option value="+">+</option>
            <option value="-">-</option>
            <option value="*">*</option>
            <option value="/">/</option>
            </select>
            <input v-model="input2" type="number" placeholder="Numero 2" />
        </div>
        <button @click="calculateResult">Calcular</button>
        <div v-if="result !== null" class="result">
            Resultado: {{ result }}
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                input1: '',
                input2: '',
                operation: '+',
                result: null,
            };
        },
        watch: {
            input1: 'calculateResult',
            input2: 'calculateResult',
            operation: 'calculateResult',
        },
        methods: {
            calculateResult() {
                const num1 = parseFloat(this.input1);
                const num2 = parseFloat(this.input2);
                if (isNaN(num1) || isNaN(num2)) {
                    this.result = 'Por favor, insira numeros validos';
                    return;
                }
                switch (this.operation) {
                    case '+':
                    this.result = num1 + num2;
                    break;
                    case '-':
                    this.result = num1 - num2;
                    break;
                    case '*':
                    this.result = num1 * num2;
                    break;
                    case '/':
                    this.result = num2 !== 0 ? num1 / num2 : 'Divisao por zero nao e permitida';
                    break;
                    default:
                    this.result = 'Operaçao nao suportada';
                }
            },
        },
    };
</script>

<style scoped>
    .calculator {
        display: flex;
        flex-direction: column;
        max-width: 300px;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }
    .display {
        display: flex;
        flex-direction: column;
        margin-bottom: 10px;
    }
    .display input,
    .display select {
        margin: 5px 0;
        padding: 10px;
        font-size: 1em;
        border: 1px solid #ccc;
        border-radius: 3px;
    }
    .result {
        margin-top: 10px;
        font-size: 1.2em;
        font-weight: bold;
    }
    button {
        padding: 10px;
        font-size: 1.2em;
        border: none;
        background-color: #28a745;
        color: white;
        cursor: pointer;
        border-radius: 3px;
    }
    button:hover {
        background-color: #218838;
    }
</style>
