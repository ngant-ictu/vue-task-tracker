<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <router-view :showAddTask="showAddTask"/>
    <Footer />
  </div>
  
</template>
<script>
import Header from "@/components/Header";
import Footer from "@/components/Footer"

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data() {
    return {
      showAddTask: false,
    }
  },
  methods: {

    toggleAddTask() {
      console.log('click');
      this.showAddTask = !this.showAddTask
    }
  }
}
</script>
<style>

</style>
