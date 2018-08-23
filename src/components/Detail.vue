<template>
  <div class="detail">
    <h2>车辆编号:{{$route.params.id}}</h2>
    <h2>故障信息:{{$route.params.detail}}</h2>
    <div class="inputbox">
      <input type="radio" v-model="method"  name="wx" value="更换二维码" />更换二维码
      <input type="radio" v-model="method"  name="wx" value="更换车胎" />更换车胎
      <input type="radio" v-model="method"  name="wx" value="其他配件" />其他配件
    </div>
    <button class="success" @click="wxwc">维修完成</button>
    <button @click="back" >返回</button>
  </div>
</template>

<script>

export default {
  name: 'Detail',
  data:function () {
    return{
      method:[],
      radio: ''
    }
  },
  methods:{
    wxwc(){
      let id = this.$route.params.id;
      let method = this.method;
      fetch(`/api/repair?id=${id}&method=${method}`).then((res)=>{
          return res.json();
      }).then((res)=>{
          console.log(res);
          if(res.message){
            alert(res.message);
            this.$router.push({path:'/'});
          }
      })
    },
    back(){
      this.$router.push({path:'/'})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  h2{
    text-align: left;
    padding-left: 5%;
    display: block;
    font-size: 1.5em;
  }
  .detail{
    background: url("../assets/home_bg2.jpg")no-repeat center bottom;
    background-size: 100% 50%;
  }
  .inputbox{
    text-align: left;
    padding-left: 5%;
  }
  input{
    margin: 20px 10px 0;
    color: #606266;
    font-weight: 500;
    cursor: pointer;
    outline: 0;
    text-align: left;
  }
  button{
    width: 90%;
    display: inline-block;
    line-height: 1;
    white-space: nowrap;
    cursor: pointer;
    background: #f4f4f5;
    border: 1px solid #d3d4d6;
    color: #909399;
    -webkit-appearance: none;
    text-align: center;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    outline: 0;
    margin: 20px auto 0;
    -webkit-transition: .1s;
    transition: .1s;
    font-weight: 500;
    padding: 12px 20px;
    font-size: 14px;
    border-radius: 4px;
  }
  .success{
    color: #409EFF;
    background: #ecf5ff;
    border-color: #b3d8ff;
  }
</style>
