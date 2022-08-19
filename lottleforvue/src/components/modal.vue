<template>
  <div>
    <div class="modal fade" ref="modal" id="myModal">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">請問確定要抽獎嗎?</h5>
          </div>
          <div class="modal-body-import">
            <p>確定要抽獎嗎?</p>
            <input
              class="import-url"
              type="text"
              style="display: none"
              value="https://docs.google.com/spreadsheets/d/e/2PACX-1vTpOQfCGnMmPhaDC9iZrrf9az33x1KX43bICyWKSaYSMOejOdXK5KYc0f3PAh6BGAsPq1bzUNClRZYQ/pub?output=csv"
            />
            <div class="warning-text">此欄位不可空白。</div>
          </div>
          <div class="modal-footer-x">
            <button
              class="btn modal-footer-btn import-btn"
              type="button"
              @click="confirm"
            >
              確認
            </button>
            <button
              class="btn modal-footer-btn cancel-btn"
              type="button"
              data-bs-dismiss="modal"
            >
              取消
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" ref="two">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">轉蛋結果?</h5>
          </div>
          <div class="modal-body-import">
            <p>{{ results }}</p>
            <input
              class="import-url"
              type="text"
              style="display: none"
              value="https://docs.google.com/spreadsheets/d/e/2PACX-1vTpOQfCGnMmPhaDC9iZrrf9az33x1KX43bICyWKSaYSMOejOdXK5KYc0f3PAh6BGAsPq1bzUNClRZYQ/pub?output=csv"
            />
            <div class="warning-text">此欄位不可空白。</div>
          </div>
          <div class="modal-footer-x">
            <button
              class="btn modal-footer-btn import-btn"
              type="button"
              @click="Closed"
            >
              確認
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" ref="third">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">遊戲紀錄</h5>
          </div>
          <div class="modal-body-import">
            <div
              class="column"
              v-for="(item, index) in GameResult"
              :key="index"
            >
              <div>{{index+1}}.</div>
              <div>{{item}}</div>
            </div>

            <input
              class="import-url"
              type="text"
              style="display: none"
              value="https://docs.google.com/spreadsheets/d/e/2PACX-1vTpOQfCGnMmPhaDC9iZrrf9az33x1KX43bICyWKSaYSMOejOdXK5KYc0f3PAh6BGAsPq1bzUNClRZYQ/pub?output=csv"
            />
            <div class="warning-text">此欄位不可空白。</div>
          </div>
          <div class="modal-footer-x">
            <button
              class="btn modal-footer-btn import-btn"
              type="button"
              @click="Closed"
            >
              確認
            </button>
          </div>
        </div>
      </div>
    </div>
     <div class="modal fade" ref="fourth">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">確定要重設嗎?</h5>
          </div>
          <div class="modal-body-import">
            <input
              class="import-url"
              type="text"
              style="display: none"
              value="https://docs.google.com/spreadsheets/d/e/2PACX-1vTpOQfCGnMmPhaDC9iZrrf9az33x1KX43bICyWKSaYSMOejOdXK5KYc0f3PAh6BGAsPq1bzUNClRZYQ/pub?output=csv"
            />
            <div class="warning-text">此欄位不可空白。</div>
          </div>
          <div class="modal-footer-x">
            <button
              class="btn modal-footer-btn import-btn"
              type="button"
              @click="resetlottle"
            >
              確認
            </button>
          </div>
        </div>
      </div>
    </div>
     <div class="modal fade" ref="list">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">獎項列表</h5>
          </div>
          <div class="modal-body-import">
            <div
              class="column"
               v-for="(item, index) in lottlearray"
              :key="index"
            >
              <div>{{item.title}}</div>
              <div>{{item.item}}</div>
            </div>

            <input
              class="import-url"
              type="text"
              style="display: none"
              value="https://docs.google.com/spreadsheets/d/e/2PACX-1vTpOQfCGnMmPhaDC9iZrrf9az33x1KX43bICyWKSaYSMOejOdXK5KYc0f3PAh6BGAsPq1bzUNClRZYQ/pub?output=csv"
            />
            <div class="warning-text">此欄位不可空白。</div>
          </div>
          <div class="modal-footer-x">
            <button
              class="btn modal-footer-btn import-btn"
              type="button"
              @click="Closed"
            >
              確認
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import modal from "bootstrap/js/dist/modal";

let firstmodel = "";
let secondmodel = "";
let thirdmodel = "";
let fourthmodel = "";
let listhmodel = "";

export default {
  name: "BoostrapModal",
  props: {
    classes: String,
    results: String,
    GameResult: Array,
  },
  data() {
    return {
      modal: null,
      lottlearray: [
        {
          title: "A賞",
          item: "角色模型"
        },
        {
          title: "B賞",
          item: "角色模型"
        },
        {
          title: "C賞",
          item: "掛軸"
        },
        {
          title: "D賞",
          item: "盤子(O)"
        },
        {
          title: "E賞",
          item: "迷你角色模型"
        },
        {
          title: "F賞",
          item: "迷你簽名板"
        },
        {
          title: "G賞",
          item: "軟塑膠吊飾"
        },
      ]
    };
  },
  watch: {
    classes(newval) {
      if (newval === "L1") {
        firstmodel.hide();
        secondmodel.show();
        thirdmodel.hide();
        fourthmodel.hide();
        listhmodel.hide();
      }
      else if (newval === "L2") {
        firstmodel.hide();
        secondmodel.hide();
        thirdmodel.show();
        fourthmodel.hide();
        listhmodel.hide();
      }
      else if (newval === "L3") {
        firstmodel.hide();
        secondmodel.hide();
        thirdmodel.hide();
        fourthmodel.show();
        listhmodel.hide();
      }
      else if (newval === "L4") {
        firstmodel.hide();
        secondmodel.hide();
        thirdmodel.hide();
        fourthmodel.hide();
        listhmodel.show();
      }
    },
  },
  created() {
    // 在 created 的時候在 Vue 底下註冊監聽 alert:message 這個事件
    this.$bus.$on("alert:message", (msg) => {
      this.showModal();
      console.log(msg);
    });
    this.$bus.$on("reset", (msg) => {
      console.log(msg);
    });
  },
  methods: {
    Closed() {
      secondmodel.hide();
      thirdmodel.hide();
      listhmodel.hide();
      this.$emit("dialogconfirm");
    },
    resetlottle() {
      fourthmodel.hide();
      this.$emit("resetlottle","")
    },
    showModal() {
      firstmodel.show();
    },
    confirm() {
      this.$emit("test");
      firstmodel.hide();
    },
    hideModal() {},
  },
  mounted() {
    console.log(this.$refs.modal);
    secondmodel = new modal(this.$refs.two);
    firstmodel = new modal(this.$refs.modal);
    thirdmodel = new modal(this.$refs.third);
    fourthmodel = new modal(this.$refs.fourth);
    listhmodel = new modal(this.$refs.list);
    console.log(thirdmodel);
    // thirdmodel.show();
  },
  beforeDestroy: function () {
    // 元件銷毀前要註銷監聽事件
    this.$bus.$off("alert:message");
    this.$bus.$off("reset");
  },
};
</script>

<style scoped>
.modal .modal-dialog {
  position: relative;
}
.modal .modal-dialog .modal-content {
  border-radius: 20px;
  background: #633b4b;
  border: 10px solid #633b4b;
  -webkit-box-shadow: 0 0 20px #633b4b;
  box-shadow: 0 0 20px #633b4b;
}
.modal .modal-dialog .modal-header {
  width: 100%;
  background: #f7524b;
  color: #fff;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  padding: 20px 35px;
  border-radius: 10px 10px 0 0;
}
.modal .modal-dialog .modal-header h5 {
  font-size: 1.5rem;
}
.modal .modal-dialog .modal-body,
.modal .modal-dialog .modal-body-import,
.modal .modal-dialog .modal-body-about {
  width: 100%;
  font-size: 2rem;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  padding: 20px 35px;
  padding-bottom: 50px;
  background: #fcf0f0;
  border-radius: 0 0 10px 10px;
}
.modal .modal-dialog .modal-body-import {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
}
.modal .modal-dialog .modal-body-import p {
  font-size: 2rem;
  font-family: FakePearl-Regular;
  font-weight: 900;
  color: #633b4b;
}
.modal .modal-dialog .modal-body-import input[type="text"] {
  padding: 10px;
  border-radius: 15px;
  border: 5px solid #633b4b67;
  outline: none;
  font-family: FakePearl-Regular;
  font-weight: 900;
  color: #3d242e;
}
.modal .modal-dialog .modal-body-import input[type="text"].warning {
  background: #f7514b27;
  border-color: #f7524b;
  color: #3e1411;
}
.modal .modal-dialog .modal-body-import .warning-text {
  font-size: 1.8rem;
  color: #f7524b;
  font-family: FakePearl-Regular;
  font-weight: 900;
  margin-top: 5px;
  display: none;
}
.modal .modal-dialog .modal-body-about {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
}
.modal .modal-dialog .modal-body-about .item {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  margin: 0;
  margin-bottom: 5px;
  padding: 0;
}
.modal .modal-dialog .modal-body-about .item p {
  padding: 0;
  margin: 0;
  font-size: 2rem;
  font-family: FakePearl-Regular;
  font-weight: 900;
  color: #633b4b;
}
.modal .modal-dialog .modal-body-about .item a {
  font-size: 2rem;
  font-family: FakePearl-Regular;
  font-weight: 900;
}
.modal .modal-dialog .modal-footer-x {
  border: none;
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 100%;
  -webkit-transform: translate(-50%, 55%);
  transform: translate(-50%, 55%);
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: space-evenly;
  -ms-flex-pack: space-evenly;
  justify-content: space-evenly;
}

.modal .modal-body-about {
  font-family: FakePearl-Regular;
  font-weight: 900;
  width: 100%;
  font-size: 2rem;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}
.modal .modal-body-record {
  width: 100%;
  display: block;
  padding: 20px 35px;
  padding-bottom: 50px;
  background: #fcf0f0;
  border-radius: 0 0 10px 10px;
}
.modal .modal-body-record .column {
  font-family: FakePearl-Regular;
  font-weight: 900;
  width: 100%;
  font-size: 2rem;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}

.modal .modal-dialog .modal-footer-x .modal-footer-btn {
  font-size: 2rem;
  font-family: FakePearl-Regular;
  color: #fff;
  font-weight: 900;
  background: #f7524b;
  padding: 10px 30px;
  border-radius: 50px;
  border: 10px solid #633b4b;
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
  -webkit-transition: 0.5s;
  transition: 0.5s;
}
.modal .modal-dialog .modal-footer-x .modal-footer-btn:hover {
  border: 10px solid #633b4b;
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
.modal .modal-dialog .modal-footer-x .modal-footer-btn:focus {
  border: 10px solid #633b4b;
  background: #c5413d;
  -webkit-transform: scale(1);
  transform: scale(1);
}
.modal .modal-dialog .modal-footer-x .cancel-btn {
  background: #fff;
  color: #633b4b;
}
.modal .modal-dialog .modal-footer-x .cancel-btn:focus {
  background: #fcdddc;
}
.modal h5,
.modal .modal-body {
  font-family: FakePearl-Regular;
  font-weight: 700;
}

@media screen and (max-width: 992px) {
  .modal .modal-dialog .modal-header {
    padding: 20px;
  }
  .modal .modal-dialog .modal-body,
  .modal .modal-dialog .modal-body-import,
  .modal .modal-dialog .modal-body-about {
    padding: 20px;
    padding-bottom: 45px;
  }
}

.column {
    font-family: FakePearl-Regular;
    font-weight: 900;
    width: 100%;
    font-size: 2rem;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
}

.column div{
    padding: 5px;;
}
</style>