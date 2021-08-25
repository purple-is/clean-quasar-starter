<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <div class="q-gutter-sm row items-start">
        <q-uploader
          url="http://localhost:4444/upload"
          style="max-width: 300px"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex'
}
</script>
