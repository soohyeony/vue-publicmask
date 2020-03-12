<template>
    <div class="container">
    <h3>User List</h3>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Username</th>
          <th scope="col">Email</th>
          <th scope="col">City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" v-bind:key="user.id"> 
          <th scope="row">{{user.id}}</th>
          <td>{{user.name}}</td>
          <td>{{user.username}}</td>
          <td>{{user.email}}</td>
          <td>{{user.address.city}}</td>
        </tr>
      </tbody>
    </table> 
  </div> 
</template>

<script>
//5. Create an API call : 데이터를 받기 위해서 axios라는 것을 사용함
//5-1. yarn을 이용하여 axios를 설치 후 import
//yarn add axios
import axios from 'axios';

//5-2. data() :users를 null로 설정해둔 다음, api 응답으로부터 받은 유저데이터를 저장하기위한 변수
// created: api를 호출하기위한(API call) axios의 get 메소드 
export default {
    name: 'Users',
    data(){
        return {
            users: null,
        };
    },
    created: function(){
        axios
        .get('https://jsonplaceholder.typicode.com/users')
        .then(res => {
            this.users = res.data;
        })
    }
}
</script>

<style>
    h3 {
        margin-bottom: 5%;
    }
</style>