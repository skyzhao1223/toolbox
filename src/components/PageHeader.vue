<template>
  <nav class>
    <div class="logo">TOOL BOX</div>
    <ul>
      <li>
        <a class="link" href="#">Github</a>
      </li>
      <li>
        <a class="link" href="#">Donate</a>
      </li>
    </ul>
  </nav>
</template>
<script>
export default {};
</script>
<style lang="scss" scoped>
nav {
  height: 66px;
  line-height: 66px;
  box-shadow: 0 0 2px 0 rgba(0, 35, 90, 0.04);
  background-color: white;
  overflow: hidden;
  padding: 0 120px;
  color: #4a4a4a;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
  font-size: 16px;
  position: fixed;
  width: 100%;
  left: 0;
  top: 0;
}
.logo {
  display: inline-block;
  background-image: url(~@/assets/logo-toolbox.svg);
  background-position: 0 17px;
  background-repeat: no-repeat;
  background-size: 32px;
  padding-left: 48px;
  font-size: inherit;
}
nav ul {
  display: inline-block;
}
nav ul li {
  display: inline-block;
  margin-left: 36px;
}
.link {
  color: inherit;
  font-size: inherit;
}
</style>
