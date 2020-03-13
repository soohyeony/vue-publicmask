<template>
    <div class="container">
    <h3>코로나19 공적 마스크😷 재고현황</h3>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">약국명</th>
          <th scope="col">상세주소</th>
          <th scope="col">재고현황</th>
          <th scope="col">입고시간</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="store in stores" v-bind:key="store.id"> 
          <th scope="row">{{store.name}}</th>
          <td>{{store.addr}}</td>
          <td>{{store.remain_stat}}</td>
          <td>{{store.stock_at}}</td>
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

//5-2. data() :stores를 null로 설정해둔 다음, api 응답으로부터 받은 데이터를 저장하기위한 변수
// created: api를 호출하기위한(API call) axios의 get 메소드 
export default {
    name: 'Users',
    data(){
        return {
            stores: null,
        };
    },
    created: function(){
        const API_URL = 'https://8oi9s0nnth.apigw.ntruss.com/corona19-masks/v1/storesByAddr/json';
        axios
        .get(`${API_URL}`)
        .then(response => {
            console.log(response.data.stores);
            this.stores = response.data.stores;
        })
    }
}
</script>

<style>
    h3 {
        margin-bottom: 5%;
    }
</style>