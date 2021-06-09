<template>
<div>
  <v-container>
    <!-- Inicio do form com filtro -->
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row>
        <v-col class="col-4">
          <v-text-field v-model="text" :rules="nameRules" label="Palavra chave" required></v-text-field>
        </v-col>
        <v-col class="col-8">
          <v-text-field v-model="name" :rules="nameRules" label="Name" required></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-text-field v-model="cep" :rules="nameRules" label="CEP" required></v-text-field>
        </v-col>
        <v-col>
          <v-text-field v-model="estado" :rules="nameRules" label="Estado" required></v-text-field>
        </v-col>
        <v-col>
          <v-text-field v-model="cidade" :rules="nameRules" label="Cidade" required></v-text-field>
        </v-col>
        <v-col>
          <v-text-field v-model="bairro" :rules="nameRules" label="Bairro" required></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-select :items="items" label="Filtrar por Escolaridade" outlined></v-select>
        </v-col>
        <v-col>
          <v-select :curso="items" label="Filtrar por Cursos" outlined></v-select>
        </v-col>
        <v-col>
          <v-select v-model="areaFilt" :items="area" label="Filtrar por Areas" outlined></v-select>
        </v-col>
        <v-col>
          <v-select v-model="tecnologias" :items="tecs" label="Filtrar por Tecnologias" outlined></v-select>
        </v-col>
      </v-row>
      <v-btn color="grey" small class="col-5" @click="reset">
        Limpar
      </v-btn>
      <v-btn color="grey" small class="col-5 ml-4">
        Filtrar
      </v-btn>
    </v-form>
    <!-- Fim do form -->
  </v-container>
  <v-simple-table class="blue-grey bd" height="400px">
    <thead>
      <tr>
        <th class="text-left">
          Nome
        </th>
        <th>
          Expectativa Salarial
        </th>
        <th>
          Gênero
        </th>
        <th>
          Personalidade
        </th>
        <th>
          Disponibilidade
        </th>
        <th>
          Endereço
        </th>
        <th class="text-right">
          Ver
        </th>
      </tr>
    </thead>
    <tbody id="filt">
      <!-- Informações dos candidatos dentro da tr/th -->
      <tr v-for="cand in filterCands" :key="cand.id">
        <th class="text-left">
            {{ cand.name }}
        </th>
        <th>
          {{ cand.salaryExpec }}
        </th>
        <th>
          {{ cand.gender }}
        </th>
        <th>
          {{ cand.personality }}
        </th>
        <th>
          {{ cand.dispo }}
        </th>
        <th>
          {{ cand.endereco }}
        </th>
        <th class="text-right">
          <!-- Link que vai para a pagina de perfil e envia as informações do candidato selecionado -->
          <nuxt-link :to="{ name: 'perfil', params: { id: cand }}" class="mx-2" small color="primary" style="text-decoration: none">
            <v-icon dark>
              mdi-plus
            </v-icon>
          </nuxt-link>
        </th>
        <!-- fim da th -->
      </tr>
    </tbody>
  </v-simple-table>
  </div>
</template>
<script>
import Cand from '../MOCK_DATA'
export default {

   components: {
     Cand
   },
   data() {
     return {
       bairro: '',
       name: '',
       tecnologias: '',
       areaFilt: '',
       cands: Cand,
       area: [
        'Desenvolvimento de Software',
        'Recrutamento de seleção',
        'Administração',
        'Administração de empresas',
        'Desenvolvimento Front-End',
        'Desenvolvimento Back-End',
        ],
        tecs: [
          'Javascript',
          'NodeJS',
          'Word',
          'Ruby',
          'Photoshop',
          'EXCEL',
        ]
     }
  },computed: {
    filterCands: function(){
      return this.cands.filter((cand) => {
        var lTec = []
        var tec = ''
        var lArea = []
        var area = ''

      //percorrer lista de tecnologias
        cand.technologies.forEach(nome =>{
          lTec.push(nome.name)
        })

      //percorrer a lista de areas
        cand.aresa.forEach(nome =>{
          lArea.push(nome.name)
        })
      //Se a Tecnologia/Area existir, o valor vazio será preenchido
      if(lTec.includes(this.tecnologias)){
        tec = this.tecnologias
      }
      if(lArea.includes(this.areaFilt)){
        area = this.areaFilt
      }
      //retorna os dados do json semelhantes ao digitado no input
      return cand.name.match(this.name) && tec.match(this.tecnologias) && area.match(this.areaFilt)
      })


    }
  },
  methods: {
      //reseta o form
      reset () {
        this.name = ''
        this.tecnologias = ''
        this.areaFilt = ''

      },
    }
  }
</script>
<style scoped>
.bd{
    border:solid 2px;
  }
</style>
