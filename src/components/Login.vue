<template>
  <div>
    <input
      v-model="name"
      type="text"
    />
    <input
      v-model="pwd"
      type="password"
    />
    <button @click="login">登陆</button>
  </div>
</template>
<script>
import * as signalR from '@aspnet/signalr'
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      name: "123456",
      pwd: "e10adc3949ba59abbe56e057f20f883e",
      staffId: ""
    };
  },
  methods: {
    login() {
      axios
        .post(
          `http://localhost:50170/api/LabourLogin/LabourLogin?Phone=${this.name}&Password=${this.pwd}`
        )
        .then(data => {
          data = data.data;
          if (data.isSuccess) {
            //保存staffId
            this.staffId = data.data.staffID;
            localStorage.setItem("UserInfo", JSON.stringify(data.data));
            //跳转主页

            //主页中进行socket连接
           // let thisVue = this;

            this.connection = new signalR.HubConnectionBuilder()
              .withUrl(
                `http://localhost:50170/api/chatHub?userId=${this.staffId}`
              )
              .configureLogging(signalR.LogLevel.Information)
              .build();

            
            this.connection.on("ToCaller", function(msg) {

              console.log(msg);
            });

            this.connection.start().then(() => {
              alert("连接成功");
              this.connection.invoke("hello").catch(function(err) {
                return console.error(err);
              });
            });
          }
        })
        .catch(err => {});
    }
  }
};
</script>
