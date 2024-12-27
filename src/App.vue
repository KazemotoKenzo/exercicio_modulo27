<script setup>
import { reactive } from "vue";

const estado = reactive({
  numA: 0,
  numB: 0,
  operador: ''
});

const operacao = () => {
  const {operador, numA, numB} = estado;
  const numeroA = Number(numA);
  const numeroB = Number(numB);

  switch (operador) {
    case '*':
      return numeroA * numeroB;
    case '-':
      return numeroA - numeroB;
    case '/':
      return dividirPorZero() ? 'NaN' : numeroA / numeroB;
    default:
      return numeroA + numeroB;
  }
}

const dividirPorZero = () => {
  return (estado.operador === '/' && estado.numB === '0')
}

</script>

<template>
  <div class="container">
    <section class="p-5 mb-4 mt-4 bg-light rounded-3">
      <form>
        <h1 class="mb-5">Calculadora Aritimética</h1>

        <div class="row">
          <div class="col-3">
            <h4 class="m">Insira um número</h4>
          </div>
          <div class="col-2">
            <h4>Operador</h4>
          </div>
          <div class="col-3">
            <h4 class="m">Insira um número</h4>
          </div>
          <div class="col-4">
            <h4>Resultado</h4>
          </div>
        </div>
        
        <div class="row">
          <div class="col-3">
            <input type="number" @keyup="evento => estado.numA = evento.target.value" class="form-control">
          </div>
          <div class="col-2">
            <select @change="evento => estado.operador = evento.target.value" class="form-control">
              <option value="+">+</option>
              <option value="-">-</option>
              <option value="*">*</option>
              <option value="/">/</option>
            </select>
          </div>
          <div class="col-3">
            <input :class="{invalido:dividirPorZero()}" type="number" @keyup="evento => estado.numB = evento.target.value" class="form-control">
            <span class="invalidado" v-if="dividirPorZero()">Não é possível dividir por 0</span>
          </div>
          <div class="col-4">
            <div :class="{invalido:dividirPorZero()}" class="form-control">{{ operacao() }}</div>
          </div>
        </div>
      </form>
    </section>
  </div>
</template>

<style scoped>
.invalido{
  outline: red;
  border-color: red;
}
.invalidado{
  color: red;
}
</style>
