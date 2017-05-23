<template>
  <div id="app">
    <!--<router-view></router-view>-->
    <div class="container">
      <div class="page-header">
        <h1>Flex Out</h1>
      </div>
      <div class="panel panel-default">
        <div class="panel-heading">
          <h3 class="panel-title">Add Category</h3>
        </div>
        <div class="panel-body">
          <form id="form" class="form-inline" v-on:submit.prevent="addCategory">
            <div class="form-group">
              <label for="categoryName">Name</label>
              <input type="text" id="categoryName" class="form-control" v-model="newCategory.name" required>
              <button type="submit" class="btn btn-default">Submit</button>
            </div>
          </form>
        </div>
      </div>
      <div class="panel panel-default">
        <div class="panel-heading">
          <h3 class="panel-title">Categories List</h3>
        </div>
        <div class="panel-body">
          <table class="table table-striped table-bordered">
            <thead>
            <tr>
              <th>Category</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="category in categories">
              <td>{{category.name}}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Firebase from 'firebase'

  let config = {
    apiKey: 'AIzaSyBk898TROH1shRmaBahVUBPUzxE1PXZpo8',
    authDomain: 'flex-ecb5c.firebaseapp.com',
    databaseURL: 'https://flex-ecb5c.firebaseio.com',
    projectId: 'flex-ecb5c',
    storageBucket: 'flex-ecb5c.appspot.com',
    messagingSenderId: '179251097845'
  }

  let app = Firebase.initializeApp(config)
  let db = app.database()

  let categoriesRef = db.ref('categories')

  export default {
    name: 'app',
    firebase: {
      categories: categoriesRef
    },
    data () {
      return {
        newCategory: {
          name: ''
        }
      }
    },
    methods: {
      addCategory: function () {
        categoriesRef.push(this.newCategory)
        this.newCategory.name = ''
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
}
</style>
