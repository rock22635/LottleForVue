<template>
  <div class="function-menu">
    <div class="btn btn-menu">
      <p>選單</p>

      <font-awesome-icon icon="fa-solid fa-angle-down" />
    </div>

    <div class="btn btn-about">
      <p>關於</p>

      <font-awesome-icon icon="fa-solid fa-info-circle" />
    </div>
    <div class="btn btn-clear" @click="reset">
      <p>重抽</p>
      <font-awesome-icon icon="fa-solid fa-arrow-rotate-left"  />
    </div>
  </div>
</template>

<script>
export default {
  name: "FunctionMenu",
  methods:{
    reset() {
      this.$emit("reset","");
      // this.$bus.$emit("reset", "");
    }
  }
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
</style>