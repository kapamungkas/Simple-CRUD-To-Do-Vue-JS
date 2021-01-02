<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <input type="text" v-model="to_do_name" class="form-control">
      </div>
      <div class="col-md-4">
        <button class="btn btn-success" v-if="mode_edit" v-on:click="onUpdate()">SAVE</button>
        <button class="btn btn-primary" v-on:click="onSubmit()">ADD TO DO</button>
      </div>
      <div class="col-md-12">
        <br>
        <table class="table">
          <tr>
            <th>ID</th>
            <th>TO DO</th>
            <th>ACTION</th>
          </tr>
          <tr v-for="(to_do_data,index) in to_do_datas" ::key="to_do_data.id">
            <td>{{ to_do_data.id }}</td>
            <td> {{ to_do_data.name }}</td>
            <td width="20%">
              <button class="btn btn-primary" v-on:click="viewData(index)">EDIT</button>
              <button class="btn btn-danger" v-on:click="deleteData(index)">DELETE</button>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import 'bootstrap/dist/css/bootstrap.min.css';

  export default {
    name: 'App',
    data() {
      return {
        to_do_name: '',
        to_do_datas: [{
          id: 1,
          name: "Create a car"
        }, {
          id: 2,
          name: "Create a bike"
        }],
        mode_edit:false,
        selected_id:0,
      }
    },
    methods: {
      onSubmit: function () {
        this.to_do_datas.push({
          id: Math.floor(Math.random() * (100 - 1 + 1)) + 1,
          name: this.to_do_name
        })
        this.mode_edit = false
        this.resetForm()
      },
      onUpdate: function(){
        this.to_do_datas[this.selected_id].name = this.to_do_name
        this.resetForm()
      },
      viewData: function (index) {
        this.to_do_name = this.to_do_datas[index].name
        this.selected_id = index
        this.mode_edit = true
      },
      deleteData: function(index){
        this.to_do_datas.splice(this.to_do_datas.indexOf(index), 1);
      },
      resetForm: function(){
        this.mode_edit = false
        this.to_do_name = ''
      }
    },
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>