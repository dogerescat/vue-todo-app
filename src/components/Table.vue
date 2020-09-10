<template>
  <div id="table">
    <label>
      <input type="radio" name="radio" value="全て" checked />全て
    </label>
    <label>
      <input type="radio" name="radio" value="作業中" />作業中
    </label>
    <label>
      <input type="radio" name="radio" value="完了" />完了
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
        <tr v-for="todo in todos" v-bind:key="todo.id">
          <td>{{todo.id}}</td>
          <td>{{todo.comment}}</td>
          <td>
            <button>{{todo.status}}</button>
          </td>
          <td>
            <button>削除</button>
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
      comment: ''
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
  },
};
</script>
<style>
table {
  margin: 0 auto;
}
</style>