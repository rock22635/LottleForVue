<template>
  
  <div id="app" ref="main">
    <div class="playtimes">遊玩次數:{{ playtimes }}</div>
    <div class="recordbtn" @click="showclass = 'L2'">獎項紀錄</div>
    <GashPon ref="gashpon"></GashPon>
    <div class="buttons">
      <div class="text">{{ Lottle }}</div>
      <div class="energy" ref="energy"></div>
    </div>
    <FunctionMenu @reset="reset" @list="list"></FunctionMenu>
    <BoostrapModal
      ref="modal"
      @test="test"
      @dialogconfirm="dialogconfirm"
      @resetlottle="init"
      :classes="showclass"
      :results="results"
      :GameResult="GameResult"
      :resultarray="resultarray"
      :Rowarray="lottlearray"
    ></BoostrapModal>
    <image-list @slime="slime" @micky="micky" @nil="nil" :selected="selected"/>
    <!-- <div class="imgcontainer">
      <div
        class="img"
        @click="slime"
        :style="selected === 1 ? 'opacity:1' : 'opacity:0.6'"
      >
        子堯版扭蛋機
        <div class="slime"></div>
      </div>
      <div
        class="img"
        @click="micky"
        :style="selected === 2 ? 'opacity:1' : 'opacity:0.6'"
      >
        羽云版扭蛋機
        <div class="micky"></div>
      </div>
      <div
        class="img"
        @click="nil"
        :style="selected === 3 ? 'opacity:1' : 'opacity:0.6'"
      >
        Nil版扭蛋機
        <div class="nil"></div>
      </div>
    </div> -->
  </div>
</template>

<script>
import GashPon from "@/components/gashpon.vue";
import FunctionMenu from "@/components/functionmenu.vue";
import BoostrapModal from "@/components/modal.vue";
import imageList from "@/components/image-list.vue"

// 滑鼠點擊位置
let mouseClick_Y = 0;

// 滑鼠移動時位置
let mouseMove_Y = 0;

// 轉蛋機縮放值
let gashaponScale_X = 0;
let gashaponScale_Y = 0;

export default {
  name: "App",
  components: {
    GashPon,
    FunctionMenu,
    BoostrapModal,
    imageList,
  },
  data() {
    return {
      Lottle: "請點扭蛋機開始遊戲",
      isPlaying: false,
      mousestaste: false,
      modalstate: false,
      playtimes: 0,
      LottleArray: [],
      showclass: "",
      results: "",
      GameResult: [],
      selected: 0,
      lottlearray: [
        {
          title: "A賞",
          count: 2,
        },
        {
          title: "B賞",
          count: 2,
        },
        {
          title: "C賞",
          count: 3,
        },
        {
          title: "D賞",
          count: 4,
        },
        {
          title: "E賞",
          count: 6,
        },
        {
          title: "F賞",
          count: 7,
        },
        {
          title: "G賞",
          count: 8,
        },
      ],
      smilearray: [
        {
          title: "A賞-惡魔史萊姆公仔",
          count: 2
        },
        {
          title: "B賞-通行百萬公仔",
          count: 2,
        },
        {
          title: "C賞-天使史萊姆公仔",
          count: 2,
        },
        {
          title: "D賞-史萊姆掛軸",
          count: 3,
        },
        {
          title: "E賞-盤子恭喜你當盤子",
          count: 4,
        },
        {
          title: "F賞-Q版模型",
          count: 5,
        },
        {
          title: "G賞-Q版吊飾",
          count: 6,
        },
        {
          title: "H賞-簽名板",
          count: 7,
        },
      ],
      mickyarray: [
        {
          title: "A賞-場地圭介 絨毛娃娃",
          count: 2,
        },
        {
          title: "B賞-佐野万次郎 絨毛娃娃",
          count: 2,
        },
        {
          title: "C賞-龍宮寺堅 絨毛娃娃",
          count: 2,
        },
        {
          title: "D賞-松野千冬 絨毛娃娃",
          count: 2,
        },
        {
          title: "E賞-花垣武道 絨毛娃娃",
          count: 2,
        },
        {
          title: "F賞-三ツ谷隆 絨毛娃娃",
          count: 2,
        },
        {
          title: "G賞-長毛巾",
          count: 4,
        },
        {
          title: "H賞-壓克力立牌",
          count: 6,
        },
        {
          title: "I賞-吊飾",
          count: 6,
        },
      ],
      nilarray: [
        {
          title: "A賞-碇真嗣模型",
          count: 2,
        },
        {
          title: "B賞-凌波零模型",
          count: 2,
        },
        {
          title: "C賞-明日香模型",
          count: 2,
        },
        {
          title: "D賞-真希波模型",
          count: 2,
        },
        {
          title: "E賞-渚薰模型",
          count: 2,
        },
        {
          title: "F賞-卡片",
          count: 4,
        },
        {
          title: "G賞-杯墊",
          count: 6,
        },
        {
          title: "H賞-吊飾",
          count: 8,
        },
      ],
      resultarray:[
        "A賞-角色模型",
        "B賞-角色模型",
        "C賞-掛軸",
        "D賞-盤子(O)",
        "E賞-迷你角色模型",
        "F賞-迷你簽名板",
        "G賞-軟塑膠吊飾",
      ]
    };
  },
  mounted() {
    this.init();
  },
  watch: {
    LottleArray(val) {
      if (val.length === 0) this.init();
    },
  },
  methods: {
    slime() {
      this.selected = 1;
      let array = [];
      let lottlearray=[];
      this.smilearray.forEach((item) => {
        lottlearray.push(item.title);
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      this.lottlearray = this.smilearray;
      this.resultarray = lottlearray;
      this.LottleArray = array;
      this.GameResult = [];
      this.playtimes = 0;
    },
    micky() {
      this.selected = 2;
      let array = [];
      let lottlearray=[];
      this.mickyarray.forEach((item) => {
        lottlearray.push(item.title);
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      this.lottlearray = this.mickyarray;
      this.resultarray = lottlearray;
      this.LottleArray = array;
      this.GameResult = [];
      this.playtimes = 0;
    },
    nil() {
      this.selected = 3;
      let array = [];
      let lottlearray=[];
      this.nilarray.forEach((item) => {
        lottlearray.push(item.title);
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      this.lottlearray = this.nilarray;
      this.resultarray = lottlearray;
      this.LottleArray = array;
      this.GameResult = [];
      this.playtimes = 0;
    },
    reset() {
      this.showclass = "L3";
    },
    list() {
      this.showclass = "L4";
    },
    init() {
      this.GameResult = [];
      this.playtimes = 0;
      this.LottleArray = [];
      this.lottlearray.forEach((item) => {
        for (let i = 0; i <= item.count - 1; i++) {
          this.LottleArray.push(item.title);
        }
      });
    },
    dialogconfirm() {
      this.mousestaste = false;
      this.modalstate = false;
      this.showclass = "";
    },
    mouseDown(e) {
      this.dialogconfirm();
      // alert(123);
      // eslint-disable-next-line
      // debugger;
      if (!this.modalState) {
        // 「變形」與「變形時間」重置
        this.gashaponScale("reset");

        // 暫停動畫定重置
        this.gashaponAnimation("stop");
        console.log(mouseClick_Y);
        mouseClick_Y = e.pageY;

        this.mousestaste = true;
      }
    },
    gashaponScale(x) {
      this.$refs.gashpon.Scale(x);
    },
    gashaponAnimation(y) {
      this.$refs.gashpon.Animation(y);
    },
    mouseMove(e) {
      if (this.mousestaste && !this.modalstate) {
        this.$refs.gashpon.$refs.main.classList.remove("default-animation");
        // $(".gashapon-main").removeClass("default-animation");

        // 游標位移量（負值向下、正值向上）
        mouseMove_Y = mouseClick_Y - e.pageY;

        gashaponScale_X = -(mouseMove_Y * 0.0005 - 1);
        gashaponScale_Y = mouseMove_Y * 0.001 + 1;
        const gashaponScale_CSS =
          "scale(" + gashaponScale_X + "," + gashaponScale_Y + ")";

        this.$refs.gashpon.$refs.main.style.transform = gashaponScale_CSS;
        // $(".gashapon-main").css("transform", gashaponScale_CSS);

        if (mouseMove_Y < 0) {
          console.log(mouseMove_Y);
          // $(".energy-bar").css("transform", "scaleY(" + mouseMove_Y / -350 + ")");
          // $(".hint-text .energy").css(
          //   "transform",
          //   "scaleX(" + mouseMove_Y / -350 + ")"
          // );
          this.$refs.energy.style.transform =
            "scaleX(" + mouseMove_Y / -350 + ")";
        }
        if (mouseMove_Y < -350) {
          this.Lottle = "可放開轉蛋機";
        } else {
          this.Lottle = "請往下拉動";
        }
      }
    },
    getRandom(x) {
      return Math.floor(Math.random() * x);
    },
    mouseUp() {
      if (this.mousestaste) {
        if (mouseMove_Y <= 0 && mouseMove_Y < -100) {
          this.gashaponScale("rebound-high");
          this.Lottle = "按住螢幕滑動";
        }
        // mouseMove_Y（正值向上拉，往下回彈變矮）
        else if (mouseMove_Y > 0 && mouseMove_Y > 100) {
          this.gashaponScale("rebound-short");
          this.Lottle = "按住螢幕滑動";
        }
        // 其他還原不回彈
        else {
          this.gashaponScale("reduction");
          this.Lottle = "按住螢幕滑動";
        }

        if (mouseMove_Y < -350 || mouseMove_Y > 350) {
          // this.modalState = true;
          this.gashaponAnimation("play");
          setTimeout(() => {
            this.gashaponAnimation("drop");
          }, 1.25 * 1000);
          this.Lottle = "顯示結果";
          // playtimes++;
          this.playtimes++;
          this.modalstate = true;
          setTimeout(() => {
            this.showModal();
          }, 3000);
        }
      }
      this.mousestaste = false;
      mouseMove_Y = 0;
      console.log(this.mousestaste);
    },

    showModal() {
      this.showclass = "L1";
      const resultindex = this.getRandom(this.LottleArray.length - 1);
      var result = this.LottleArray[resultindex];
      this.LottleArray.splice(resultindex, 1);
      this.results = result;
      this.GameResult.push(result);
    },
    test() {
      this.Lottle = "按住螢幕往下滑動";
      this.isPlaying = true;
      this.$refs.main.addEventListener("mousedown", this.mouseDown);
      this.$refs.main.addEventListener("touchstart", this.mouseDown);
      this.$refs.main.addEventListener("mousemove", this.mouseMove);
      this.$refs.main.addEventListener("touchmove", this.mouseMove);

      this.$refs.main.addEventListener("mouseup", this.mouseUp);
      this.$refs.main.addEventListener("mouseleave", this.mouseUp);
      this.$refs.main.addEventListener("touchend", this.mouseUp);
    },
  },
};
</script>

<style>
@font-face {
  font-family: FakePearl-Regular;
  src: url(https://cdn.jsdelivr.net/gh/max32002/FakePearl@1.1/webfont/FakePearl-Regular.woff2)
      format("woff2"),
    url(https://cdn.jsdelivr.net/gh/max32002/FakePearl@1.1/webfont/FakePearl-Regular.woff)
      format("woff");
}

:root {
  --play-number: 1;
  --play-number-drop: 1;
  --play-number-rotate: 1;
  --play-state: paused;
  --play-state-drop: paused;
  --play-state-rotate: paused;
  --play-duration: 1800ms;
  --play-duration-drop: 3000ms;
  --play-duration-rotate: 1800ms;
}

html,
body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  overflow: hidden;
  font-size: 10px;
}

div {
  /* border: 1px solid black; */
}

#app {
  width: 100%;
  height: 100vh;
  font-family: FakePearl-Regular;
  background: radial-gradient(#ffc68a 25%, #fdd98d 10%);
  background-size: 20px 20px;
  -webkit-animation: scales 100s infinite linear;
  -webkit-animation-animation: scales 100s infinite linear;
}

.playtimes {
  position: absolute;
  z-index: 9;

  font-weight: 900;
  font-size: 2.5rem;
  color: #8d5b5b;
  top: 10%;
  left: 50%;
  transform: translateX(-50%);
}
.buttons {
  position: absolute;
  bottom: 10%;
  font-weight: 900;
  font-size: 1.5rem;
  color: #fcf0f0;
  border: 8px solid #633b4b;
  border-radius: 50px;
  background: #8d5b5b;
  padding: 10px 25px;
  cursor: pointer;
  left: 50%;
  transform: translateX(-50%);
  overflow: hidden;
}

.buttons .energy {
  position: absolute;
  width: 100%;
  height: 100%;
  background: #633b4b;
  top: 0%;
  left: 0%;
  -webkit-transform: scaleX(0);
  transform: scaleX(0);
  z-index: -1;
  transform-origin: 0% 100%;
}

.buttons .text {
  min-width: 200px;
  text-align: center;
}

.recordbtn {
  position: absolute;
  left: 50%;
  top: 3%;
  transform: translatex(-50%);
  font-size: 1.3rem;
  padding: 9px;
  border-radius: 10%;
  background: #8d5b5b;
  color: white;
  cursor: pointer;
  z-index: 2;
}



@keyframes scales {
  0% {
    background-position: 0px 0px;
  }
  100% {
    background-position: 100% 100%;
  }
}
</style>
