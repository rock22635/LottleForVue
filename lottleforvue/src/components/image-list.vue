<template>
  <div class="imgcontainer" ref="menubox">
    <div @click="openlist" class="btnlist">扭蛋機列表</div>
    <transition name="fade">
      <div class="imgblock" v-show="MenuStatus" @click="$emit('slime')">
        子堯版扭蛋機
        <div
          class="slime"
          :style="selected === 1 ? 'opacity:1' : 'opacity:0.6'"
        ></div>
      </div>
    </transition>
    <transition name="fade">
      <div class="imgblock" @click="$emit('micky')" v-show="MenuStatus">
        羽云版扭蛋機
        <div
          class="micky"
          :style="selected === 2 ? 'opacity:1' : 'opacity:0.6'"
        ></div>
      </div>
    </transition>
    <transition name="fade">
      <div
      @click="$emit('nil')"
      class="imgblock"
      v-show="MenuStatus"
    >
      Nil版扭蛋機
      <div class="nil" :style="selected === 3 ? 'opacity:1' : 'opacity:0.6'"></div>
    </div>
    </transition>
    
  </div>
</template>

<script>
export default {
  props: {
    selected: Number,
  },
  data: function () {
    return {
      MenuStatus: false,
    };
  },
  methods: {
    openlist() {
      this.MenuStatus = !this.MenuStatus;
      if (!this.MenuStatus) {
        this.$refs.menubox.classList.remove("close");
        this.$refs.menubox.classList.add("open");
      } else {
        this.$refs.menubox.classList.remove("open");
        this.$refs.menubox.classList.add("close");
      }
    },
  },
};
</script>


<style scoped>
.imgcontainer {
  z-index: 9;
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

.imgblock{
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

.btnlist{
  background: #8d5b5b;
  color: white;padding: 4px;
  border-radius: 10%;
  width:133px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>