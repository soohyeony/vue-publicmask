<template>
    <div class="container">
    <h4>코로나19 공적 마스크😷 재고현황</h4>
    <p>
      <b>주소를 입력하세요(동까지만):</b>
    </p>
      <input type="text" v-model.lazy="addrInput" placeholder="경기도 성남시 분당구 운중동">
      <button type="button" class="btn" @click="pharmSearch">검색</button>

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
          <td id="remainStat">{{store.remain_stat}}</td>
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
//https://8oi9s0nnth.apigw.ntruss.com/corona19-masks/v1/storesByAddr/json?address=서울특별시%20중구
export default {
    name: 'Users',
    data(){
        return {
            stores: null,
            addrInput: '',
            addrReplace: ''
        };
    },
    methods:{
      // blankReplace: function(){
      //   this.addrReplace = this.addrInput.replace(/(\s*)/g, "%20");
      // },
      pharmSearch: function(){
        //공백을 %20으로 replace
        this.addrReplace = this.addrInput.replace(/(\s*)/g, "%20");
        const API_URL = `https://8oi9s0nnth.apigw.ntruss.com/corona19-masks/v1/storesByAddr/json?address=${this.addrInput}`;
        axios
        .get(`${API_URL}`)
        .then(response => {
            //console.log(response.data.stores);
            this.stores = response.data.stores;
        })
      }
    },
    // computed:{
    //   statColor: function(){
    //     var statEmoji = {
    //       "plenty":"🟢100개 이상",
    //       "some":"🟡30개 이상 100개 미만",
    //       "few":"🔴2개 이상 30개 미만",
    //       "empty": "⚪1개 이하",
    //       "break":"❌판매중지"
    //     };
    //     var statTxt = document.getElementById("remainStat").innerHTML;
    //     for (var i=0; i < statEmoji.length; i++){
    //       if(statTxt == statEmoji[i])
    //         return statTxt = statEmoji[statTxt];
    //     }
    //   }
    // }
}
</script>

<style>
    h4 {
        width: 100%;
        margin-bottom: 5%;
        background-color: black;
        color: lightgray;
        padding: 10px;
        font-weight: bold;
    }

    .btn{
      background-color: green;
      margin: 10px;
      color: white;
      font-weight: bold;
    }

    input[type=text]{
      border: none;
      border-bottom: 2px solid black;
      width: 80%;
      padding: 10px 10px;
      font-size: 20px;
      transition: 0.5s;
    }

    input[type=text]:focus {
      border-bottom: 2px solid green;
      outline: none;
    }
</style>