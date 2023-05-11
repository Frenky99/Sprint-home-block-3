<template>
  <q-page class="q-px-xl">
    <h2 class="text-center">Todo</h2>
    <q-list>
      <div>
        <q-input
          @keyup.enter="addTask"
          rounded
          outlined
          v-model="addToNote"
          placeholder="enter a note"
        >
          <template v-slot:append>
            <q-btn @click="addTask" round dense flat icon="add" />
          </template>
        </q-input>
      </div>
      <!-- clickable делает так, чтобы чек бокс снова нажимался, если бы мы не прописывали все это, то у нас бы не отрабатывала стилистика при нажатии на галку -->
      <q-item
        clickable
        @click="task.done = !task.done"
        class="shadow-5 q-my-md"
        :class="{ 'done bg-pink-3': task.done }"
        v-for="(task, index) in tasks"
        :key="task.id"
      >
        <q-item-section avatar>
          <!-- class="no-pointer-events" чтобы при клике у нас не нажималась галочка, связана с clickable -->
          <q-checkbox
            class="no-pointer-events"
            v-model="task.done"
            val="teal"
            color="teal"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label class="text-italic text-weight-medium">
            {{ task.title }}</q-item-label
          >
        </q-item-section>
        <!-- side будет отрабатывать когда действие выполнено -->
        <q-item-section v-if="task.done" side>
          <q-btn
            @click="clickDelete(index)"
            class="no-shadow"
            icon="delete"
          ></q-btn>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>
  
<script>
export default {
  data() {
    return {
      addToNote: "",
      tasks: [
        { title: "Unicorn 1", done: false, id: 1 },
        { title: "Unicorn 2", done: false, id: 2 },
        { title: "Unicorn 3", done: false, id: 3 },
      ],
    };
  },
  methods: {
    clickDelete(index) {
      this.$q
        .dialog({
          title: "Delete Todo",
          message: "Delete party note?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify({
            message: "Note deleted",
            color: "pink-4",
            icon: "info",
          });
        });
    },
    addTask() {
      this.tasks.push({
        title: this.addToNote,
        done: false,
      });
      this.addToNote = "";
    },
  },
};
</script>

<style lang="scss">
.q-page-container {
  background: #facbe9;
}

.done {
  .q-item__label {
    color: grey;
    text-decoration: line-through;
  }
}
.q-item {
  border-radius: 10px;
}

.q-checkbox__inner--truthy {
  color: var(--q-primary) !important;
}

.q-btn:before {
  box-shadow: none;
}
</style>
