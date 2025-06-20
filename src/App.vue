<script setup>
import { ref } from 'vue';
import { startData } from './utils/startData.js';
import InputGridle from './components/InputGridle.vue'
import CalkGrille from './components/CalkGrille.vue'
import DetailsGrille from './components/DetailsGrille.vue'
import RequestMaterials from './components/RequestMaterials.vue'
import EquipmentSheet from './components/EquipmentSheet.vue'
import MaterialsWorkshop from './components/MaterialsWorkshop.vue'
import SaveTables from './components/SaveTables.vue'
import DrawOptimisation from './components/DrawOptimisation.vue'
import WerticalAuto from './components/WerticalAuto.vue'

const grille = ref(startData.grille)
const details = ref(startData.details)
const material = ref(startData.material)
const products = ref(startData.products)
const department = ref(startData.department)
function add_property() {
  department.value = material.value.map((profileItem) => {
    const foundOriginalMaterial = material.value.find(
      (mat) => mat.articul === profileItem.articul
    );
    return {
      ...profileItem,
      color: foundOriginalMaterial.color, // Если нужна прямая ссылка на объект
      department: "ЦАК",
    };
  });
}

</script>

<template>

  <main>
    {{ add_property() }}
    <InputGridle v-model:grille="grille" />
    <CalkGrille v-model:grille="grille" v-model:details="details" v-model:material="material"
      v-model:products="products" v-model:department="department" /> 
    <DetailsGrille v-model:details="details" />
    <RequestMaterials v-model:material="material" />
    <EquipmentSheet v-model:products="products" />
    <MaterialsWorkshop v-model:department="department" />
    <SaveTables v-model:grille="grille" v-model:details="details" v-model:material="material"
      v-model:products="products" v-model:department="department" />
    <DrawOptimisation v-model:material="material" />
    <WerticalAuto/>

  </main>
</template>
