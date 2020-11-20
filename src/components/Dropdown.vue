<template>
  <div>
    <div class="input-group-prepend">
      <button
        v-if="infoLists[0] === 'กรุงเทพมหานคร'"
        class="btn btn-outline-secondary dropdown-toggle dropdownBtn"
        type="button"
        data-toggle="dropdown"
        aria-haspopup="true"
        aria-expanded="false"
      >
        <i class="fas fa-map-marker-alt"></i> พื้นที่ใกล้ฉัน
      </button>
      <button
        v-else
        class="btn btn-outline-secondary dropdown-toggle dropdownBtn"
        type="button"
        data-toggle="dropdown"
        aria-haspopup="true"
        aria-expanded="false"
      >
        กรุณาเลือก
      </button>
      <div class="dropdown-menu">
        <div v-for="(list, index) in infoLists" :key="index">
          <a class="dropdown-item" href="#">{{ list }}</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    infoLists: Array,
  },
};
</script>

<style>
/* .dropdown-menu {
  position: absolute;
  height: 150px;
} */
.dropdownBtn {
  border-radius: 0.25rem;
  border-color: rgb(211, 207, 207);
}
</style>