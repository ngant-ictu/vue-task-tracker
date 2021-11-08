<template>
  <div>
    <div v-show="showAddTask">
      <AddTask @new-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTaskAction" :tasks="tasks" />
  </div>
</template>

<script>
import Tasks from "@/components/Tasks"
import AddTask from "@/components/AddTask"

export default {
  name: 'Home',
  components: {
    Tasks,
    AddTask,
  },
  props: {
    showAddTask: Boolean
  },
  data() {
    return {
      tasks: [],
    }
  },
  methods: {

    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(task)
      })
      console.log('res', res);
      const data = await res.json();
      console.log('data', data)
      this.tasks = [...this.tasks, data]
    },

    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const upTask = { ...taskToToggle, reminder: !taskToToggle.reminder }
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(upTask)
      })
      const data = await res.json();
      this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder: data.reminder} : task)
    },
    async deleteTaskAction(id) {
      if (confirm('Are you sure?')){
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        })
        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error deleting task')
        
      }
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
      const data = res.json();
      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
  }
}
</script>
