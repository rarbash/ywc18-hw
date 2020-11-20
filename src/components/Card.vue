<template>
  <div class="cardBox">
    <div v-for="(merchantsList, name) in merchantsLists" :key="name">
      <div class="card mb">
        <div class="card-body cardBody">
          <div>
            <img
              :src="merchantsLists[name].coverImageId"
              alt="resturant_img"
              class="cardimg"
            />
          </div>
          <div class="cardInfo">
            <div class="d-flex">
              <h4 class="smfont">
                <strong>{{ merchantsLists[name].shopNameTH }}</strong>
              </h4>
              <div v-if="merchantsLists[name].isOpen === 'Y'">
                <button
                  type="button"
                  class="btn btnOpen"
                  style="background-color: limegreen; color: white"
                >
                  เปิดอยู่
                </button>
              </div>
              <div v-if="merchantsLists[name].isOpen === 'N'">
                <button type="button" class="btn btn-secondary btnOpen">
                  ปิดแล้ว
                </button>
              </div>
            </div>
            <div class="d-flex flex-wrap">
              <div class="colorSilver mrCard">
                {{ merchantsLists[name].subcategoryName }}
              </div>
              <div class="colorSilver mrCard">|</div>
              <div class="d-flex flex-row">
                <div v-for="(price, num) in priceRang" :key="num">
                  <i
                    class="fas fa-dollar-sign notActiveColor"
                    v-if="merchantsLists[name].priceLevel <= num"
                  ></i>
                  <i class="fas fa-dollar-sign" v-else></i>
                </div>
              </div>
              <div class="colorSilver mrCard mlCard">|</div>
              <div class="d-flex">
                <div class="colorSilver mrCard">
                  {{ merchantsLists[name].addressDistrictName }}
                </div>
                <div class="colorSilver">
                  {{ merchantsLists[name].addressProvinceName }}
                </div>
              </div>
            </div>
            <hr />
            <div
              class="colorSilver text-left"
              v-html="merchantsLists[name].highlightText"
            ></div>
            <div class="d-flex flex-wrap">
              <div class="mtCard" style="margin: 0.5rem 0.3rem 0 0">
                <strong>สินค้าแนะนำ:</strong>
              </div>
              <div class="d-flex flex-wrap">
                <span class="mtCard colorSilver">{{
                  merchantsLists[name].recommendedItems.join(", ")
                }}</span>
              </div>
            </div>
            <div class="d-flex">
              <div
                class="colorSilver2"
                v-for="(facilitie, item) in merchantsLists[name].facilities"
                :key="item"
              >
                <i
                  class="fas fa-parking fa-2x icon"
                  v-if="facilitie === 'ที่จอดรถ'"
                ></i>
                <i
                  class="fas fa-dog fa-2x icon"
                  v-if="facilitie === 'สามารถนำสัตว์เลี้ยงเข้าได้'"
                ></i>
                <i
                  class="fas fa-book fa-2x icon"
                  v-if="facilitie === 'รับจองล่วงหน้า'"
                ></i>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-if="name === 4">
        <button
          type="button"
          class="btn btn-outline-secondary btn-light moreInfoBtn"
        >
          ดูเพิ่มเติม
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import "@fortawesome/fontawesome-free/js/all.js";
import "@fortawesome/fontawesome-free/css/all.css";
export default {
  props: {
    merchantsLists: Array,
    merchantsNameLists: Array,
  },
  data() {
    return {
      priceRang: [1, 2, 3, 4],
    };
  },
  watch: {
    merchantsNameLists() {
      console.log("send", this.merchantsNameLists);
    },
  },
};
</script>

<style>
/* .cardBox {
  display: grid;
  row-gap: 15px;
} */
.cardBody {
  display: flex;
  padding: 6px;
}
.cardimg {
  width: 300px;
  height: 300px;
  margin-right: 10px;
  border-radius: 0.25rem;
  object-fit: cover;
}
.cardInfo {
  padding: 20px;
}
.d-flex {
  display: flex;
}
.icon {
  color: limegreen;
  margin: 1.3rem 0.5rem 0 0;
}
.notActiveColor,
.colorSilver {
  color: silver;
}
.btnOpen {
  padding: 0.1rem;
  border-radius: 3px;
  font-size: 0.8rem;
  margin-left: 1rem;
}
.mtCard {
  margin-top: 0.5rem;
}
strong {
  color: #2c3e50;
}
.mrCard {
  margin-right: 0.3rem;
}
.mlCard {
  margin-left: 0.3rem;
}
.mb {
  margin-bottom: 1rem;
}
.moreInfoBtn {
  margin-top: 1.5rem;
  justify-self: center;
  border-color: rgb(211, 207, 207);
  height: 3rem;
  width: 20rem;
}
@media only screen and (max-width: 768px) {
  .cardBody {
    display: grid;
    padding: 0px;
  }
  .smfont {
    font-size: 1rem;
  }
  .cardInfo {
    padding: 1rem;
  }
  .cardimg {
    margin-right: 0;
    width: 100%;
    height: 200px;
  }
  .moreInfoBtn {
    width: 100%;
  }
}
</style>