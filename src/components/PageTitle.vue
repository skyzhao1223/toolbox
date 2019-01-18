<template>
  <div class="tb-title">
    <span class="tb-title-name"><span class="logo icon-nowrap t">{{$route.meta.title}}</span>{{$route.meta.title}}</span>
    <!-- <router-link class="tb-title-menu" to="/" exact></router-link> -->
  </div>
</template>
<style lang="scss" scoped>
.tb-title {
  line-height: 80px;
  font-size: 16px;
  display: flex;
  height: 80px;
  justify-content: space-between;
  align-items: center;
}
.tb-title .logo {
  border-radius: 1px;
  margin-right: 9px;
  background-color: #9aa7b9;
  display: inline-block;
  line-height: 19px;
  font-size: 8px;
  color: white;
  height: 18px;
  width: 22px;
  position: relative;
  top: 2.5px;
}
.icon-nowrap {
  text-transform: uppercase;
  word-break: break-all;
  text-align: center;
  overflow: hidden;
}
.tb-title-menu {
  background-image: url(~@/assets/menu.svg);
  background-size: 16px;
  height: 16px;
  width: 16px;
  position: relative;
  top: 2px;
}
</style>
