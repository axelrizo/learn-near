<template>
  <section id="course-video">
    <div class="container">
      <b-row>
        <b-col class="actions-col d-flex flex-column flex-sm-row justify-content-between mb-2">
          <b-button
            id="content-btn"
            v-b-toggle.content-sidebar
            class="purple-btn"
          >
            <BaseIcon
              height="12"
              width="14"
              class="mr-2"
            >
              <ContentIcon />
            </BaseIcon>
            Contenido
          </b-button>
          <b-sidebar
            id="content-sidebar"
            title="Contenido del curso"
            shadow
            bg-variant="dark"
            text-variant="light"
            class="mt-5"
          >
            <div class="px-3 py-2">
              <CourseModules />
            </div>
          </b-sidebar>
          <div class="d-flex justify-content-between mt-2 mt-sm-0">
            <div class="auto-play-switch custom-switch p-0">
              <p class="mb-0 switch-name">
                AUTO PLAY
              </p>
              <label class="switch">
                <input
                  id="autoplay"
                  v-model="autoplay"
                  type="checkbox"
                >
                <span class="slider" />
              </label>
            </div>
            <div class="d-flex ml-4">
              <b-button class="prev-next-btn purple-btn mr-2">
                <BaseIcon
                  height="10"
                  width="10"
                  style="transform: rotate(180deg);"
                >
                  <PreviousIcon />
                </BaseIcon>
              </b-button>
              <b-button class="prev-next-btn purple-btn">
                <BaseIcon
                  height="10"
                  width="10"
                >
                  <NextIcon />
                </BaseIcon>
              </b-button>
            </div>
          </div>
        </b-col>
        <b-col cols="12">
          <h1>{{ lessonName }}</h1>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <slot name="video" />
        </b-col>
      </b-row>
    </div>
  </section>
</template>

<script>
import ContentIcon from '@/components/icons/ContentIcon.vue'
import NextIcon from '@/components/icons/NextIcon.vue'
import PreviousIcon from '@/components/icons/PreviousIcon.vue'
export default {
  name: 'CourseVideo',
  components: {
    ContentIcon,
    NextIcon,
    PreviousIcon
  },
  data () {
    return {
      autoplay: false,
      videoURL: null
    }
  },
  computed: {
    lessonName () {
      const lessonStore = this.$store.state.course_watch.currentLesson
      if (lessonStore && lessonStore.lessonUri === this.$route.params.lessonid) {
        return lessonStore.lessonName
      }
      return 'Presentación del curso'
    }
  }
}
</script>

<style scoped>
#course-video {
  background-color: var(--dark-gray-5);
  padding-top: 32px;
}

.actions-col .purple-btn {
  background-color: var(--light-blue-1);
  border-color: var(--light-blue-1);
}

/*switch*/
.switch-name {
  color: var(--light-gray-1);
  font-size: 12px;
}

.switch {
  position: relative;
  display: inline-block;
  width: 100%;
  height: 20px;
  margin-bottom: 0;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  -webkit-transition: .4s;
  transition: .4s;
  border-radius: 12px;
}

.slider:before {
  color: var(--light-gray-1);
  position: absolute;
  content: "off";
  height: 100%;
  width: 50%;
  left: 0;
  bottom: 0;
  background-color: var(--light-blue-1);
  transition: .4s;
  border-radius: 12px;
  font-size: 12px;
  text-align: center;
}

#autoplay + .slider{
  background-color: var(--dark-gray-2);
}

#autoplay:checked + .slider {
  background-color: var(--dark-gray-2);
}

input:checked + .slider:before {
  -webkit-transform: translateX(100%);
  -ms-transform: translateX(100%);
  transform: translateX(100%);
  border-radius: 12px;
  content: "on";
}

.actions-col #content-btn {
  border-radius: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 34px;
  width: 148px;
}

.actions-col .prev-next-btn {
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 36px;
  width: 36px;
}

h1 {
  color: var(--light-gray-1);
  font-size: 1.5rem;
  font-weight: 800;
}
</style>
