<template>
  <q-page>
    <div v-for="component in blueprint">
    {{ component}}
      <component
        :is="component.whichComponent"
        :class="component.theClass"
        :style="component.style"
        :size="component.size"
        :label="component.label"
        :src="component.src"
        :spinner-color="component.spinner-color || ''"
      />
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      blueprint: [
        {
          whichComponent: 'q-btn',
          theClass: 'q-ma-md',
          label: 'q-btn',
          size: 'xl'
        },
        {
          whichComponent: 'q-img',
          src: 'https://icatcare.org/app/uploads/2018/07/Thinking-of-getting-a-cat.png',
          class: 'q-pa-xl'
        },
      ]
    }
  }
}
</script>
