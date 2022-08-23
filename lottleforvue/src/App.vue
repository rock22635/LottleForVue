<template>
  <div id="app" ref="main">
    <div class="playtimes">遊玩次數:{{ playtimes }}</div>
    <div class="recordbtn" @click="showclass = 'L2'">歷史紀錄</div>
    <GashPon ref="gashpon"></GashPon>
    <div class="buttons">
      <div class="text">{{ Lottle }}</div>
      <div class="energy" ref="energy"></div>
    </div>
    <FunctionMenu @reset="reset" @list="list"></FunctionMenu>
    <BoostrapModal
      @test="test"
      @dialogconfirm="dialogconfirm"
      @resetlottle="init"
      :classes="showclass"
      :results="results"
      :GameResult="GameResult"
    ></BoostrapModal>
    <div class="imgcontainer">
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

      <!-- <img src="./assets/01_bg.jpg" alt=""> -->
    </div>
  </div>
</template>

<script>
import GashPon from "@/components/gashpon.vue";
import FunctionMenu from "@/components/functionmenu.vue";
import BoostrapModal from "@/components/modal.vue";

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
          count: 3,
        },
        {
          title: "B賞",
          count: 3,
        },
        {
          title: "C賞",
          count: 3,
        },
        {
          title: "D賞",
          count: 6,
        },
        {
          title: "E賞",
          count: 6,
        },
        {
          title: "F賞",
          count: 28,
        },
        {
          title: "G賞",
          count: 31,
        },
      ],
      smilearray: [
        {
          title: "A賞-惡魔史萊姆公仔",
          count: 2,
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
          count: 6,
        },
        {
          title: "F賞-Q版模型",
          count: 6,
        },
        {
          title: "G賞-Q版吊飾",
          count: 28,
        },
        {
          title: "H賞-簽名板",
          count: 31,
        },
      ],
      mickyarray: [
        {
          title: "A賞-佐野万次郎黏土人",
          count: 2,
        },
        {
          title: "B賞-花垣武道 絨毛娃娃",
          count: 2,
        },
        {
          title: "C賞-佐野万次郎 絨毛娃娃",
          count: 2,
        },
        {
          title: "D賞-龍宮寺堅 絨毛娃娃",
          count: 2,
        },
        {
          title: "E賞-松野千冬 絨毛娃娃",
          count: 2,
        },
        {
          title: "F賞-場地圭介 絨毛娃娃",
          count: 2,
        },
        {
          title: "G賞-三ツ谷隆 絨毛娃娃",
          count: 2,
        },
        {
          title: "H賞-長毛巾",
          count: 24,
        },
        {
          title: "I賞-壓克力立牌",
          count: 18,
        },
        {
          title: "J賞-吊飾",
          count: 26,
        },
      ],
      nilarray: [
        {
          title: "A賞-碇真嗣模型",
          count: 1,
        },
        {
          title: "B賞-凌波零模型",
          count: 1,
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
          count: 16,
        },
        {
          title: "G賞-杯墊",
          count: 28,
        },
        {
          title: "H賞-吊飾",
          count: 28,
        },
      ],
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
      this.smilearray.forEach((item) => {
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      this.LottleArray = array;
      this.GameResult = [];
      this.playtimes = 0;
    },
    micky() {
      this.selected = 2;
      let array = [];
      this.mickyarray.forEach((item) => {
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      this.LottleArray = array;
      this.GameResult = [];
      this.playtimes = 0;
    },
    nil() {
      // eslint-disable-next-line
      debugger;
      this.selected = 3;
      let array = [];
      this.nilarray.forEach((item) => {
        for (let i = 0; i <= item.count - 1; i++) {
          array.push(item.title);
        }
      });
      console.log(array);
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

.imgcontainer {
  position: absolute;
  top: 3%;
  left: 6%;
  text-align: center;
  font-size: 20px;
}
.img {
  opacity: 0.6;
  cursor: pointer;
}
.slime {
  background-image: url("@/assets/slime.jpg");
  height: 142px;
  width: 133px;
  background-position: center;
  background-size: cover;
  border-radius: 23px;
}

.micky {
  background-image: url("@/assets/micky.png");
  height: 142px;
  width: 133px;
  background-position: center;
  background-size: cover;
  border-radius: 23px;
}

.nil {
  background-image: url("@/assets/02.png");
  height: 142px;
  width: 133px;
  background-position: center;
  background-size: cover;
  border-radius: 23px;
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
