<template>
  <div>
    <div class="RNNXgb">
      <div class="SDkEP">
        <div class="a4bIc">
          <div class="vdLsw gsfi">
            <input
              class="gLFyf gsfi"
              maxlength="2048"
              type="text"
              v-model="message"
              placeholder="Enter the  command to run or script path"
              name="messageN"
              id="messageI"
              autocomplete="on"
              v-on:keyup.enter="submitMsg"
            >
          </div>
        </div>
      </div>
    </div>

    <center>
      <input
        value="Let's Roll"
        aria-label="Let's Roll"
        name="btnK"
        type="button"
        class="submitcss"
        @click="submitMsg"
      >
    </center>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Cmd",
  // props: {
  //   message: String
  // },
  data() {
    return {
      message: this.message == undefined ? "" : this.message,
      inputList: this.inputList == undefined ? "" : "test"
    };
  },
  // data: {
  //     inputList: []
  //   },
  methods: {
    getInputList() {
      if (localStorage.getItem("inputList")) {
        this.inputList = localStorage.getItem("inputList").split(";");
      } else {
        //localStorage.inputList=JSON.stringify([ ])
        localStorage.setItem("inputList", "");
      }
      //console.log(localStorage.getItem("inputList"))
    },

    submitMsg() {
      let cmd = this.message;
      //first cache the input into localStorage
      // if (cmd.length < 1) {
      //   //do nothing
      // } else {
      //   localStorage.setItem("inputList",this.inputList+";"+cmd)
      // }
      //console.log(this.inputList)
      //localStorage.inputList=this.inputList.push(this.message)
      //console.log(localStorage.inputList)
      // if(localStorage.inputList) {
      //   this.inputList=localStorage.inputList
      // }

      let baseURI = "http://localhost:966/runsh?cmd=";
      //var uri_enc = encodeURIComponent(baseURI+=this.message);
      //alert(uri_enc)
      //let cmd = this.message.replace(/ /g, "@"); //全局替换空格位@符号，在spring boot后端会做相反的操作
      let cmdMsg = "";
      baseURI += cmd;
      //baseURI = encodeURIComponent(baseURI)
      const options = { title: "" };

      axios
        .post(baseURI)
        .then(response => {
          cmdMsg = response.data;
          //console.log(cmdMsg);
          if (cmdMsg.length < 1) {
            cmdMsg = "May Run Successfully...";
          }
          alert(cmdMsg, options);
        })
        .catch(e => {
          alert(e.data);
        });

      //console.log(baseURI);
      //console.log(cmdMsg);
    }
  }
};
</script>

<style scoped>
.submitcss {
  border-radius: 24px;
  background: #f2f2f2;
  border: 1px solid #f2f2f2;
  color: #757575;
  cursor: default;
  font-size: 14px;
  font-weight: bold;
  width: 200px;
  padding: 40 16px;
  height: 36px;
  margin: 20px;
}

.submitcss:hover {
  background-image: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#f8f8f8),
    to(#f1f1f1)
  );
  background-image: -webkit-linear-gradient(top, #f8f8f8, #f1f1f1);
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  background-color: #f8f8f8;
  background-image: linear-gradient(top, #f8f8f8, #f1f1f1);
  background-image: -o-linear-gradient(top, #f8f8f8, #f1f1f1);
  border: 1px solid #c6c6c6;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  color: #222;
}

.SDkEP {
  flex: 1;
  display: flex;
  padding: 5px 8px 0 16px;
  padding-left: 20px;
}

.RNNXgb {
  background: #fff;
  display: flex;
  border-radius: 8px;
  border: 1px solid #dfe1e5;
  box-shadow: none;
  border-radius: 24px;
  z-index: 3;
  height: 44px;
  margin: 0 auto;
  width: 482px;
}
.RNNXgb:hover {
  box-shadow: 0 1px 6px 0 rgba(32, 33, 36, 0.28);
  border-color: rgba(223, 225, 229, 0);
}

.a4bIc {
  display: flex;
  flex: 1;
  flex-wrap: wrap;
}

.vdLsw {
  color: transparent;
  flex: 100%;
  white-space: pre;
}

.gsfi,
.lst {
  font: 16px arial, sans-serif;
  line-height: 34px;
  height: 34px !important;
}

.gLFyf {
  background-color: transparent;
  border: none;
  margin: 0;
  padding: 0;
  color: rgba(0, 0, 0, 0.87);
  word-wrap: break-word;
  outline: none;
  display: flex;
  flex: 100%;
  -webkit-tap-highlight-color: transparent;
  /* margin-top: -37px; */
  width: 482px;
}
</style>


