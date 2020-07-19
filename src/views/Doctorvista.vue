<template>
  <div>
    
    <MenuDoctor></MenuDoctor>
    
      <component v-bind:is="this.componenteVista">
      </component>
    
  </div>
</template>

<style type="scss">
@import '../css/pacientevista.css';

</style>
<script>
import MenuDoctor from '@/components/MenuDoctor.vue'
import InicioPaciente from '@/components/InicioPaciente.vue'
import PerfilDoctor from '@/components/PerfilDoctor.vue'
import ActualizarDoctor from '@/components/ActualizarDoctor.vue'
import ModificarHorarioDoc from '@/components/ModificarHorarioDoc.vue'
import AgregarHorarioDoc from '@/components/AgregarHorarioDoc.vue'
import { mapActions, mapState } from 'vuex'

export default {
    
    name: 'Doctorvista',
    components: {
      MenuDoctor,
      InicioPaciente,
      PerfilDoctor,
      ActualizarDoctor,
      ModificarHorarioDoc,
      AgregarHorarioDoc
    },
    
    computed:{
      ...mapState(['componenteVista'])
    },
    
}
</script>

<style>

</style>