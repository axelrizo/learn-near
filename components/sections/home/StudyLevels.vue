<template>
  <section
    id="study-levels"
    class="container "
  >
    <h2>Conoce los diferentes niveles de estudios</h2>
    <b-row>
      <b-col
        v-for="level in levels"
        :key="level.id"
        cols="12"
        sm="6"
        md="4"
        class="mx-auto"
      >
        <div class="level p-3">
          <NuxtLink
            :to="{ name: 'courses-level-level', params: { level: level.id }}"
          >
            <div class="d-flex justify-content-center justify-content-sm-start">
              <BaseIcon
                height="33"
                width="38"
                :class="['icon-' + level.id]"
              >
                <LevelIcon />
              </BaseIcon>
            </div>
            <p class="level-title mt-2 text-center text-sm-left">
              {{ level.level }}
            </p>
            <p class="level-text text-center text-sm-left">
              {{ level.text }}
            </p>
          </NuxtLink>
        </div>
      </b-col>
    </b-row>
  </section>
</template>

<script>
import LevelIcon from '@/components/icons/LevelIcon.vue'
export default {
  name: 'StudyLevels',
  components: {
    LevelIcon
  },
  data () {
    return {
      levels: [
        {
          id: 'basic',
          level: 'Basico',
          text: 'Conoce las bases, conceptos y todo lo que necesitas saber para configurar de forma correcta tu ecosistema NEAR.'
        },
        {
          id: 'intermediate',
          level: 'Intermedio',
          text: 'Desarrolla tus bases  y crea tus primeros proyectos de una forma profesional, empleando buenas practicas NEAR.'
        },
        {
          id: 'advanced',
          level: 'Avanzado',
          text: 'Maximiza tus proyectos e ideas de la mano de los profesionales en la tecnología NEAR.'
        }
      ]
    }
  }
}
</script>

<style scoped>
h2 {
  font-size: 1.5rem;
  font-weight: 800;
  margin-bottom: 80px;
}

.level {
  transition: all 0.3s ease-out;
}

.level:hover {
  cursor: pointer;
  transform: translateY(-5px) scale(1.005) translateZ(0);
  box-shadow: 0px 10px 15px -3px rgba(0,0,0,0.1);
}

.level a {
  color: var(--dark-gray-5);
}

.level a:hover {
  text-decoration: none;
}

.level-title {
  text-decoration: none;
  font-size: 1.2rem;
  font-weight: 800;
}

.level-text {
  font-size: .9rem;
}

.icon-basic {
  color: var(--light-orange-1);
}

.icon-intermediate {
  color: var(--light-blue-1);
}

.icon-advanced {
  color: var(--light-green-1);
}
</style>
