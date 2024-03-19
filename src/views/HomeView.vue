<script setup>
import { ref, watch, computed } from 'vue'

const height = ref(0);
const weight = ref(0);
const age = ref(0);
const sex = ref('Male');
const activityMultiplier = ref(1);
const bmi = computed(() => {
  return (weight.value / (height.value / 100) ** 2).toFixed(1)
})

const bmr = computed(() => {
  //For Men: BMR = (10 * weight in kg) + (6.25 * height in cm) - (5 * age in years) + 5
  //For Women: BMR = (10 * weight in kg) + (6.25 * height in cm) - (5 * age in years) - 161
  if (sex.value == 'Male') {
    return ((weight.value * 10) + (height.value * 6.25) - (age.value * 5) + 5).toFixed(0)
  } else {
    return ((weight.value * 10) + (height.value * 6.25) - (age.value * 5) - 161).toFixed(0)
  }
})

const tdee = computed(() => {
  return (bmr.value * activityMultiplier.value).toFixed(0)
})

</script>
<template>
  <main>
    <div class="infoContainer">
      <div class="inputContainer">
        <label for="age">Idade</label>
        <input type="number" name="age" v-model="age"  id="">
      </div>
      <div class="inputContainer">
        <label for="height">Altura(cm): </label>
        <input type="number" name="height" id="height" v-model="height">
      </div>
      <div class="inputContainer">
        <label for="weight">Peso(kg): </label>
        <input type="number" name="weight" id="weight" v-model="weight">
      </div>
      <div class="inputContainer">
        <label for="sex">Sexo</label>
        <select name="sex" id="" v-model="sex">
          <option value="Male">Homem</option>
          <option value="Female">Mulher</option>
        </select>
      </div>
      <div class="inputContainer">
        <label for="activity">Nível de Atividade</label>
        <select name="actiity" id="" v-model="activityMultiplier">
          <option value="1.2">Sedentário(a)</option>
          <option value="1.375">Atividade Leve</option>
          <option value="1.55">Atividade Moderada</option>
          <option value="1.725">Atividade Alta</option>
          <option value="1.9">Atividade Super Intensa</option>
        </select>
      </div>
    </div>
    <div class="resultContainer">
      <p class="bmi">
        IMC: {{ isNaN(bmi) ? 'Sem informações para calcular.' : bmi}}
      </p>
      <br>
      <p class="bmr">
        BMR: {{ isNaN(bmr) ? 'Sem informações para calcular.' : bmr }}
      </p>
      <p class="tdee">
        TDEE: {{ isNaN(tdee) ? 'Sem informações para calcular.' : tdee }}
      </p>
    </div>
  </main>
</template>

<style scoped>

.infoContainer {
  display: flex;
  gap: 10px;
  margin-top: 2vh;
  justify-content: center;
  flex-direction: column;
  width: 350px;
}

input {
  width: 50px;
  border-radius: 20px;
  border: 1px solid rgb(132, 0, 255);
}

.inputContainer {
  display: flex;
  justify-content: space-between;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(32, 32, 32);
  color:white;
}

</style>
