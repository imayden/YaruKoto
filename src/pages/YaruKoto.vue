<template>
  <!-- <q-page class="flex flex-center"> -->
    <q-page class="column" :style="{ backgroundColor: '#ECDAB6' }">
    <!-- <img alt="Quasar logo" src="src/assets/quasar-logo-vertical.svg" style="width: 200px; height: 200px" > -->
    <!-- <h5>YaruKoto</h5> -->

    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        :style="{ backgroundColor: '#F9F4EB' }"
        standout
        square
        filled
        placeholder="Write A New YaruKoto Task ..."
        dense>
        <!-- <template v-slot:before>
          <q-icon name="event" />
        </template>
        <template v-slot:hint>
          Write A New YaruKoto Task ...
        </template> -->

        <template v-slot:append>
          <q-btn
            @click="addTask"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>
    </div>

    <q-list
      :style="{ backgroundColor: '#F9F4EB' }"
      separator
      bordered
      >
      <!-- Rendering a <label> tag (notice tag="label"), so QCheckboxes will respond to clicks on QItems to change Toggle state. -->

      <!-- Task Card -->
        <q-item
          v-for="(task, index) in tasks"
          :key="task.title"
          @click="task.done = !task.done"
          :class="{'done' : task.done }"
          :style="{ backgroundColor: task.done ? '#F3E7D1' : '' }"
          clickable
          v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary" />
        </q-item-section>

        <!-- Task Content -->
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>

        <!-- Delete Task -->
        <q-item-section
          v-if="task.done"
          side
        >
        <q-btn
          @click.stop="deleteTask(index)"
          flat
          round
          dense
          color="primary"
          icon="delete" />
        </q-item-section>

      </q-item>

    </q-list>

    <div
      v-if="!tasks.length"
      class="no-tasks absolute-center">
      <div class="text-h6 text-primary text-center" >
        <q-icon
        name="check"
        size="100px"
        color="primary"
        />
      </div>
      <div class="text-h6 text-primary text-center" >
        Good Job! You Finished Everything!
      </div>

    </div>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  // name: 'YaruKoto',

  data(){
    return {
      newTask: '',
      tasks: [
        // {
        //   title: 'Get A Good Job',
        //   done: false,
        // },
      ]
    }
  },

  methods: {

    vibrate() {
      // Vibrate Feedback
      if ("vibrate" in navigator) {
        // Vibrate for 200ms
        navigator.vibrate(200);
      }
    },

    deleteTask(index){
      this.vibrate();
      this.$q.dialog({
        title: 'Erase or not',
        message: 'Erase this Yarukoto Task now.',
        cancel: true,
        persistent: true
      }).onOk(() => {
        console.log('>>>> Task Deleted')
        this.tasks.splice(index, 1)
        this.$q.notify({
          color: 'info',
          message: 'Task Erased!',
          icon: 'delete'
        })
      })
    },

    addTask(){
      this.vibrate();
      // Empty task detection
      if (this.newTask.trim() === '') {
        this.$q.notify({
          color: 'warning',
          message: 'Oops...Write something first!',
          icon: 'warning'
        });
        return;
      }

      console.log('>>>> Task Added')
      this.tasks.push({
        title: this.newTask,
        done: false,
      })
      this.newTask = ''
      this.$q.notify({
        color: 'positive',
        message: 'Task Added!',
        icon: 'check'
      })
    }
  }


})
</script>

<style lang="scss">

  .done{
    .q-item__label{
      text-decoration: line-through;
      color: #C6B6A5;
    }
  }

  .no-tasks{
    opacity: 0.5;
  }

</style>
