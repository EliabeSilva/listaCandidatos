<template>
<div>
  <v-simple-table class="blue-grey pa-1" height="400px">
    <h3 class="text-center bd">Perfil</h3>
    <br>
    <p>Nome: {{ perf.name }}</p>
    <p>Data de aniversário: {{ perf.birthdate }}</p>
    <p>Email: {{ perf.email }}</p>
    <p>Gênero: {{ perf.gender }}</p>
    <p>Tel: {{ perf.phone }}</p>
    <p>Etnia: {{ perf.ethnicity }}</p>
    <div v-if="perf.isDeficiency === true">
      <p>Deficiente: Sim</p>
    </div>
    <div v-else>
      <p>Deficiente: Não</p>
    </div>
    <h3 class="text-center bd">Area</h3>
    <br>
    <div v-for="aresa in perf.aresa">
      <div v-if="aresa.name.length > 0">
        <ul>
          <li>{{ aresa.name }}</li>
        </ul>
      </div>
      <div v-else>
        <ul>
          <li>Nenhum</li>
        </ul>
      </div>
    </div>
    <h3 class="text-center bd">Experiência</h3>
    <br>
    <div v-if="perf.experiences.length > 0">
      <div v-for="exp in perf.experiences">
        <p class="text-black">Nome Da Empresa: {{ exp.companyName }}</p>
        <p>Remuneração: R$ {{ exp.remuneration }},00</p>
        <p>Data de inicio: {{ exp.startDate }}</p>
        <p>Data final: {{ exp.endDate }}</p>
        <p>Descrição: {{ exp.description }}</p>
      </div>
    </div>
    <div v-else>
      <p>Sem experiência</p>
    </div>
    <h3 class="text-center bd">Tecnologias</h3>
    <br>
    <div v-if="perf.technologies.length > 0">
      <div v-for="tec in perf.technologies">
        <p>Nome Da Tec: {{ tec.name }} | Nivel: {{ tec.level }}</p>
        <br>
      </div>
    </div>
    <div v-else>
      <p>Sem Tecnologia</p>
    </div>
      <br>
  </v-simple-table>
  <v-btn to="/"
      depressed
      color="red"
      class="mt-1"
    >
      Voltar
    </v-btn>
</div>
</template>
<script>
export default {
  data() {
     return {
      perf: this.$route.params.id
     }
  }
}
</script>
<style scoped>
  .text-black{
    color: black;
  }
  p{
    font-family: 'Arial', Arial, sans-serif;
  }
  .bd{
    border:solid 2px #363636;
  }
</style>
