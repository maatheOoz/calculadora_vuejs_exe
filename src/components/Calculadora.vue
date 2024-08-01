<script setup>
import { reactive } from 'vue';

    const estado = reactive({
    primeiroNumero: '',
    segundoNumero: '',
    operacoes: {
    soma: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => (b !== 0 ? a / b : 'Zero'),
    },
    resultado: 0,
});

const calcularResultado = () => {
    const { primeiroNumero, segundoNumero, contaMatematica } = estado;
    const num1 = parseFloat(primeiroNumero);
    const num2 = parseFloat(segundoNumero);
    
    estado.resultado = !isNaN(num1) && !isNaN(num2) ? estado.operacoes[contaMatematica](num1, num2) : 'Operação inválida';
};
</script>

<template>
    <div class="container p-3 mb-2 bg-secondary text-white">
        <h1 class="mt-5 mb-3">Calculadora Aritmética</h1>
        <input class="form-control p-3 mb-2 bg-dark text-white" type="text" v-model="estado.primeiroNumero" @input="calcularResultado" />
        <input type="text" class="form-control mt-2 p-3 mb-2 bg-dark text-white" v-model="estado.segundoNumero" @input="calcularResultado" />

        <select class="mt-3 mb-1 p-3 bg-dark text-white" v-model="estado.contaMatematica" @change="calcularResultado">
            <option value="soma">Soma</option>
            <option value="subtracao">Subtração</option>
            <option value="multiplicacao">Multiplicação</option>
            <option value="divisao">Divisão</option>
        </select>
        <p>
            Resultado: {{ estado.resultado }}
        </p>
    </div>
</template>
