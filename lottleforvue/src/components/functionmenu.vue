<template>
  <div class="function-menu">
    <div class="menu-box" ref="menubox">
      <div class="btn btn-menu" @click="test">
        <p>選單</p>

        <font-awesome-icon icon="fa-solid fa-angle-down"  :rotation="MenuStatus?180:0" />
      </div>

      <div class="btn btn-abouts" style="opacity: 0;">
        <p>關於</p>

        <font-awesome-icon icon="fa-solid fa-info-circle" />
      </div>
      <div class="btn btn-reset" @click="reset" style="opacity: 0;">
        <p>重抽</p>
        <font-awesome-icon icon="fa-solid fa-arrow-rotate-left" />
      </div>
      <div class="btn btn-list" @click="list" style="opacity: 0;">
        <p>獎項</p>
        <font-awesome-icon icon="fa-solid fa-dice" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FunctionMenu",
  data() {
    return {
      MenuStatus: false,
    }
  },
  methods: {
    test() {
      if (!this.MenuStatus) {
        this.$refs.menubox.classList.remove("close");
        this.$refs.menubox.classList.add("open");
      } else {
        this.$refs.menubox.classList.remove("open");
        this.$refs.menubox.classList.add("close");
      }
      this.MenuStatus = !this.MenuStatus;
       
      
    },
    reset() {
      this.$emit("reset", "");
      // this.$bus.$emit("reset", "");
    },
    list() {
      this.$emit("list", "");
      // this.$bus.$emit("reset", "");
    },
  },
};
</script>

<style scoped>
.function-menu {
  position: absolute;
  top: 3%;
  right: 3%;
}

.function-menu .btn {
  font-size: 1.3em;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 3px;
}
.btn p {
  font-weight: 900;
  color: #633b4b;
  padding: 0;
  margin: 0;
}

.btn svg {
  width: 20px;
  height: 20px;
  padding: 20px;
  margin-left: 10px;
  border-radius: 50px;
  background: #633b4b;
  color: white;
}

.btn svg path {
  width: 12px;
}

.function-menu .menu-box {
  width: -webkit-fit-content;
  width: -moz-fit-content;
  width: fit-content;
  padding: 5px;
  position: absolute;
  top: 0;
  right: 0;
}

.function-menu .menu-box.close .btn-abouts{
  pointer-events: none;
}

.function-menu .menu-box.close .btn-reset {
  pointer-events: none;
}

.function-menu .menu-box.close .btn-list {
  pointer-events: none;
}

.function-menu .menu-box.open .btn-reset {
  pointer-events: auto;
}

.function-menu .menu-box.open .btn-list {
  pointer-events: auto;
}

.function-menu .menu-box.open .btn-abouts{
  pointer-events: auto;
}

.function-menu .menu-box .btn {
  font-size: 1.9em;
  height: 50px;
  font-family: FakePearl-Regular;
  font-weight: 900;
  color: #fff !important;
  z-index: 99;
  white-space: nowrap;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
  transition: 0.5s;
  padding: 29px 0;
}

.function-menu .menu-box .btn p {
  font-weight: 900;
  color: #633b4b;
  padding: 0;
  margin: 0;
}
.function-menu .menu-box .btn:hover i {
  background: #f7524b;
}
.function-menu .menu-box .btn i {
  width: 50px;
  height: 50px;
  font-size: 2rem;
  background: #633b4b;
  border-radius: 50px;
  margin-left: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 0.5s;
}
 .function-menu .open .btn-abouts{
        webkit-animation-name: fade-in-move; 
        animation-name: fade-in-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }

  .function-menu .close .btn-abouts{
        webkit-animation-name: fade-out-move; 
        animation-name: fade-out-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }

   .function-menu .open .btn-reset{
        webkit-animation-name: fade-in-move; 
        animation-name: fade-in-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }
  .function-menu .close .btn-reset{
        webkit-animation-name: fade-out-move; 
        animation-name: fade-out-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }

  .function-menu .open .btn-list{
        webkit-animation-name: fade-in-move; 
        animation-name: fade-in-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }
  .function-menu .close .btn-list{
        webkit-animation-name: fade-out-move; 
        animation-name: fade-out-move;
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
  }
  @-webkit-keyframes fade-in-move {
        0% {
          -webkit-transform: translateY(-40px);
                  transform: translateY(-40px);
          opacity: 0;
        }
        100% {
          -webkit-transform: translateY(0px);
                  transform: translateY(0px);
          opacity: 1;
        }
  }
  @keyframes fade-in-move {
        0% {
          -webkit-transform: translateY(-40px);
                  transform: translateY(-40px);
          opacity: 0;
        }
        100% {
          -webkit-transform: translateY(0px);
                  transform: translateY(0px);
          opacity: 1;
        }
      }
      @-webkit-keyframes fade-out-move {
        0% {
          -webkit-transform: translateY(0px);
                  transform: translateY(0px);
          opacity: 1;
        }
        100% {
          -webkit-transform: translateY(-40px);
                  transform: translateY(-40px);
          opacity: 0;
        }
      }
      @keyframes fade-out-move {
        0% {
          -webkit-transform: translateY(0px);
                  transform: translateY(0px);
          opacity: 1;
        }
        100% {
          -webkit-transform: translateY(-40px);
                  transform: translateY(-40px);
          opacity: 0;
        }
      }
</style>