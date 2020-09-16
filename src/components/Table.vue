<template>
  <div id="table">
    <label v-for="status in todoStatus" v-bind:key="status.id">
      <input type="radio" name="radio" v-bind:value="status.value" v-model="picked" />
      {{status.value}}
    </label>
    <table>
      <thead>
        <tr>
          <th>id</th>
          <th>コメント</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody id="todo-body">
        <tr v-for="(todo, index) in todos" v-bind:key="todo.id">
          <td>{{todo.id}}</td>
          <td>{{todo.comment}}</td>
          <td>
            <button>{{todo.status}}</button>
          </td>
          <td>
            <button v-on:click="deleteTask(index)">削除</button>
          </td>
        </tr>
      </tbody>
    </table>
    <h2>新規タスクの追加</h2>
    <input type="text" v-model="comment" />
    <input type="button" value="追加" v-on:click="addTask" />
  </div>
</template>
<script>
export default {
  name: 'Table',
  data() {
    return {
      todos: [],
      id: 1,
      comment: '',
      todoStatus: [
        { id: 1, value: '全て' },
        { id: 2, value: '作業中' },
        { id: 3, value: '完了' },
      ],
      picked: '全て',
    };
  },
  methods: {
    addTask() {
      this.todos.push({
        id: this.id++,
        comment: this.comment,
        status: '作業中',
      });
      this.comment = '';
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
      this.updateId();
    },
    updateId() {
      if (!this.todos.length) {
        this.id = 1;
        return;
      }
      this.todos.forEach((todo, index) => {
        todo.id = index + 1;
        this.id = todo.id + 1;
      });
    },
  },
};
</script>
<style>
table {
  margin: 0 auto;
}
</style>