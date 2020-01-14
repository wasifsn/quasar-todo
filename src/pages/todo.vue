<template>
  <q-page class="bg-grey-3 column">
    <q-input class="addTodo" @keyup.enter="addTodo" v-model="todo" label="Add Task"></q-input>
    <q-list v-for="(item,index) in todoList" :key="item.title" class="bg-white">
      <q-item class="todoItem" v-ripple>
        <q-item-section avatar>
          <input
            type="checkbox"
            @change="done(item,index)"
            :id="index"
            :value="item"
            v-model="status"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>
            <span
              class="todoText"
              :class="{completed:item.status}"
              :id="index"
              :for="index"
            >{{item.title}}</span>
          </q-item-label>
        </q-item-section>
        <q-item-section avatar>
          <q-btn @click="removeTodo(item,index)" round color="purple" glossy icon="card_giftcard" />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!todoList[0]" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="amber"></q-icon>
      <div class="text-center text-h5 text-amber">No Tasks</div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "todo",
  data: function() {
    return {
      toggle: false,
      status: [],
      todo: "",
      todoList: [
        // { title: "eat food", status: false },
        // { title: "jogging", status: false },
        // { title: "make things", status: false }
      ]
    };
  },
  methods: {
    addTodo(e) {
      let todo = e.target.value;
      this.todoList.push({ title: todo, status: false });
      this.todo = "";
      console.log(this.todoList);
    },
    removeTodo(item, index) {
      this.todoList.splice(index, 1);
      // const idToRemove = item.title;
      // const filteredItem = this.todoList.filter(
      //   item => item.title !== idToRemove
      // );
      // this.todoList = filteredItem;
    },
    done(item, index) {
      console.log(item, index);
      this.todoList[index].status = !this.todoList[index].status;
    }
  }
};
</script>
<style  scoped>
.completed {
  text-decoration: line-through;
}

.todoItem {
  border-bottom: 1px solid peachpuff;
}

.no-tasks {
  opacity: 0.5;
}
.addTodo {
  padding: 0 1rem;
}
</style>