<template>
  <div class="home">
    <ListForm />
    <List />
  </div>
</template>

<script>
import List from '@/components/List.vue'
import ListForm from '@/components/ListForm.vue'

export default {
  name: 'Home',
  components: {
    List,
    ListForm
  }
}
</script>
