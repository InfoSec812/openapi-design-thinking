<template>
  <q-page class="row q-pa-md items-start justify-start">
    <q-table class="col-grow q-" :rows="rows">
    </q-table>
  </q-page>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { TodoApi, Todo } from 'src/sdk';
import { useQuasar } from 'quasar';

const $q = useQuasar();
const rows = ref<Todo[]>([]);
const todoApi = new TodoApi();

onMounted(async () => {
  try {
    rows.value = await todoApi.getTodoList();
  } catch (error) {
    $q.notify({
      type: 'warning',
      message: `${JSON.stringify(error)}`
    })
  }
});
</script>
