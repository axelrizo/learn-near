<template>
  <div
    id="courses"
    class="container mt-5"
  >
    <h1 class="mb-5">
      Cursos
    </h1>
    <div class="filters container">
      <b-row>
        <!----
        <b-col class="search-wrapper d-flex align-items-end px-0">
          <b-input-group>
            <template #append>
              <BaseIcon icon-name="search">
                <SearchIcon />
              </BaseIcon>
            </template>
            <b-form-input
              id="search-course"
              placeholder="Búsqueda por titulo"
              autocomplete="off"
              class="search-input"
            />
          </b-input-group>
        </b-col>-->
        <b-col cols="12" class="mb-3 mb-md-0 px-0 d-flex justify-content-end">
          <b-form-group
            v-slot="{ ariaDescribedby }"
            label=""
            class="m-0"
          >
            <b-form-radio-group
              v-model="selected"
              :options="options"
              :aria-describedby="ariaDescribedby"
              class="level-btn"
              buttons
              button-variant="primary"
              name="buttons-2"
              @change="selectLevel($event)"
            />
          </b-form-group>
        </b-col>
      </b-row>
    </div>
    <div class="row mt-5">
      <template v-if="courses.length > 0">
        <b-col
          v-for="(course, index) in courses"
          :key="index"
          cols="12"
          sm="6"
          xl="3"
          class="mb-4"
        >
          <CourseCard
            :card-content="course"
          />
        </b-col>
      </template>
      <div
        v-else
        class="d-flex justify-content-center align-items-center w-100"
      >
        <b-spinner variant="secondary" label="Loading Courses" />
        <span class="ml-3 font-weight-bold">Cargando Cursos...</span>
      </div>
    </div>
  </div>
</template>

<script>
// import SearchIcon from '@/components/icons/SearchIcon.vue'
export default {
  name: 'CoursesIndex',
  components: {
    // SearchIcon
  },
  data () {
    return {
      selected: '', // Must be an array reference!
      options: [
        { text: 'Basico', value: 'basic' },
        { text: 'Intermedio', value: 'intermediate' },
        { text: 'Avanzado', value: 'advanced' }
      ],
      courses: []
    }
  },
  async fetch () {
    await this.$course.getCourses()
      .then((response) => {
        this.courses = response.data.data
      })
      .catch((error) => {
        console.log('ERROR: ', error)
      })
  },
  mounted () {
    const param = this.$route.params.level
    if (param) { this.selected = param }
  },
  methods: {
    selectLevel (opt) {
      this.$router.replace({ name: 'courses-level-level', params: { level: opt } })
    }
  }
}
</script>

<style>
.filters {
  position: relative;
  z-index: 10;
}

.filters input{
  height: 40px;
}

.search-wrapper .input-group-append {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #FFFFFF;
  cursor: pointer;
  border-radius: 0 5px 5px 0;
  border: 1px solid #ced4da;
  border-left: none;
  padding: 0 .5rem;
}
.level-btn > .btn-primary {
  color: var(--light-blue-1);
  background: transparent;
  border-color: var(--light-blue-1);
  width: 100px !important;
  padding-top: 8px;
  padding-bottom: 8px;
}
.level-btn > .btn-primary:nth-child(2){
    border-radius: 0 !important;
}
.level-btn > .btn-primary:first-child{
    border-top-right-radius: 0 !important;
    border-bottom-right-radius: 0 !important;
}
.level-btn > .btn-primary:last-child{
    border-top-left-radius: 0 !important;
    border-bottom-left-radius: 0 !important;
}
.level-btn > .btn-primary.active,
.btn-primary:not(:disabled):not(.disabled):active{
  background: var(--light-blue-1) !important;
   border-color: var(--light-blue-1) !important;
}
.search-input{
  border-top-left-radius: 100px;
  border-bottom-left-radius: 100px;
}
.search-wrapper .input-group-append{
  border-top-right-radius: 100px;
    border-bottom-right-radius: 100px;
}
</style>
