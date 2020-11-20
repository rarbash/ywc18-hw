<template>
  <div>
    <div class="nav">
      <div id="nav" class="nav-info navInfo">
        <router-link to="" class="underline">หน้าแรก</router-link> /
        <router-link to="/" class="bold">ค้นหา</router-link>
      </div>
    </div>
  </div>
</template>


<style>
.nav {
  background-color: rgb(40, 59, 124);
  position: absolute;
  left: 0;
  right: 0;
}
.navInfo {
  margin-left: 9rem;
}
.underline {
  text-decoration: underline;
}
@media only screen and (max-width: 768px) {
  .navInfo {
    margin-left: 0.1rem;
  }
}
</style>