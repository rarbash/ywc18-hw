<template>
  <div class="information">
    <div class="header">
      <img alt="คนละครึ่ง logo" class="logo" src="../assets/logo-KLK.png" />
      <img
        alt="คนละครึ่ง logo"
        class="d-none d-sm-block logoName"
        src="../assets/logo-KLKname.png"
      />
      <div class="input-group mb-3 searchGroup">
        <div class="d-none d-sm-block">
          <button
            class="btn btn-outline-secondary dropdown-toggle locationInputBtn"
            type="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <i class="fas fa-map-marker-alt"></i> พื้นที่ใกล้ฉัน
          </button>
          <div class="dropdown-menu">
            <div v-for="(list, index) in this.provincesList" :key="index">
              <a class="dropdown-item" href="#">{{ list }}</a>
            </div>
          </div>
        </div>
        <input
          type="text"
          class="form-control inputSearch"
          placeholder="ค้นหา ชื่อร้านอาหาร และเครื่องดื่ม ร้านธงฟ้าร้านOTOP และสิ้นค้าทั่วไป"
          v-model="searchInput"
        />
        <div class="input-group-append">
          <button class="btn btn-outline-secondary searchBtn" type="button">
            <i class="fas fa-search"></i>
          </button>
        </div>
      </div>
      <div class="d-block d-sm-none">
        <button
          type="button"
          class="btn fillterBtn"
          data-toggle="modal"
          data-target="#moblieModal"
        >
          <i class="fas fa-filter"></i>
        </button>
        <div
          class="modal fade"
          id="moblieModal"
          tabindex="-1"
          aria-labelledby="moblieModalLabel"
          aria-hidden="true"
        >
          <div class="modal-header filterHeader">
            <button
              type="button"
              class="btn"
              data-dismiss="modal"
              aria-label="Close"
            >
              <i class="fas fa-less-than colorWhite"></i>
            </button>
            <h2 class="colorWhite mrMoblie">กรอกผล</h2>
          </div>
          <Choice
            v-if="dataList.length !== 0"
            :categoriesLists="categoriesList"
            @onCheckedCategoryChange="onCheckedCategoryChange"
            @onCheckedSubcategoryChange="onCheckedSubcategoryChange"
            :provincesLists="provincesList"
            :priceRangeLists="priceRangeList"
            class="mobileChoice"
          />
        </div>
      </div>
    </div>
    <Navbar />
    <div>
      <div class="body">
        <h3 class="mt">ผลการค้นหา ร้านอาหารและเครื่องดื่ม ทั้งหมด</h3>
        <div class="bodyInfomation">
          <Choice
            v-if="dataList.length !== 0"
            :categoriesLists="categoriesList"
            @onCheckedCategoryChange="onCheckedCategoryChange"
            @onCheckedSubcategoryChange="onCheckedSubcategoryChange"
            :provincesLists="provincesList"
            :priceRangeLists="priceRangeList"
            class="d-none d-sm-block"
          />
          <Card
            v-if="dataList.length !== 0"
            :merchantsLists="fileredMerchantsName && fileredSubcategories"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Card from "@/components/Card.vue";
import Choice from "@/components/Choice.vue";
import axios from "axios";

export default {
  components: {
    Navbar,
    Card,
    Choice,
  },
  data() {
    return {
      dataList: [],
      categoriesList: [],
      provincesList: [],
      priceRangeList: [],
      merchantsList: [],
      searchInput: "",
      checkedCategory: "ทั้งหมด",
      checkedSubcategory: "ทั้งหมด",
    };
  },
  async mounted() {
    await this.getPanjsAPI();
  },
  computed: {
    // fileredCategories() {
    //   return this.categoriesList.filter((categorie) =>
    //     categorie.name.includes(this.checkedCategory)
    //   );
    // },
    fileredSubcategories() {
      return this.checkedSubcategory !== "ทั้งหมด"
        ? this.merchantsList.filter((subcategorie) =>
            subcategorie.subcategoryName.includes(this.checkedSubcategory)
          )
        : this.merchantsList;
    },
    fileredMerchantsName() {
      return this.searchInput !== ""
        ? this.merchantsList.filter((merchantsList) =>
            merchantsList.shopNameTH
              .toLowerCase()
              .includes(this.searchInput.toLowerCase())
          )
        : this.merchantsList;
    },
  },
  methods: {
    async getPanjsAPI() {
      try {
        const response = await axios.get("https://panjs.com/ywc18.json");
        this.dataList = response.data;
        this.categoriesList = response.data.categories;
        const responseProvinces = response.data.provinces;
        for (const state in responseProvinces) {
          this.provincesList.push(responseProvinces[state]);
        }
        const responsePriceRange = response.data.priceRange;
        for (const price in responsePriceRange) {
          this.priceRangeList.push(responsePriceRange[price]);
        }
        const responseMerchants = response.data.merchants;
        for (const merchant in responseMerchants) {
          this.merchantsList.push(responseMerchants[merchant]);
        }
      } catch (error) {
        console.log(error);
      }
    },
    onCheckedCategoryChange(value) {
      this.checkedCategory = value;
    },
    onCheckedSubcategoryChange(value) {
      this.checkedSubcategory = value;
    },
  },
};
</script>

<style>
.header {
  display: flex;
  margin-bottom: 10px;
  align-items: center;
}
.searchGroup {
  height: 10px;
  width: 70%;
}
.body {
  padding: 20px;
  display: grid;
  row-gap: 3%;
}
.bodyInfomation {
  display: grid;
  grid-template-columns: 27% 72%;
  column-gap: 20px;
}
.logo {
  width: 4rem;
  height: 3rem;
  margin-left: 10rem;
  margin-right: 6px;
  margin-top: 6px;
  object-fit: cover;
}
.logoName {
  width: 5rem;
  height: 1.5rem;
  margin-right: 6px;
  object-fit: cover;
}
h3 {
  justify-self: start;
}
.inputSearch {
  border-color: rgb(211, 207, 207);
  border-left: transparent;
  border-right: transparent;
}
.inputDropdown {
  border-radius: 1px;
}
.searchBtn {
  border-radius: 5px;
  border-left: transparent;
  border-color: rgb(211, 207, 207);
  background-color: rgb(242, 239, 239);
  width: 4rem;
}
.locationInputBtn {
  border-radius: 5px 0 0 5px;
  border-color: rgb(211, 207, 207);
}
.mt {
  margin-top: 5rem;
}
@media only screen and (max-width: 768px) {
  .inputSearch {
    border-color: rgb(211, 207, 207);
    border-left: 1px solid rgb(211, 207, 207);
  }
  .logo {
    margin-left: 1rem;
    margin-right: none;
    margin-top: 6px;
  }
  .header {
    display: grid;
    grid-template-columns: 23% 67% 10%;
    align-items: center;
  }
  h3 {
    font-size: 1rem;
  }
  .bodyInfomation {
    grid-template-columns: 100%;
  }
  .body {
    row-gap: 20px;
  }
  .searchGroup {
    width: 100%;
  }
  .mt {
    margin-top: 3rem;
  }
  .fillterBtn {
    margin-top: 1rem;
  }
  .filterHeader {
    background-color: rgb(40, 59, 124);
  }
  .colorWhite {
    color: white;
  }
  .mrMoblie {
    margin-right: 6.5rem;
  }
  /* .mobileChoice {
    margin-left: 1rem;
  } */
}
</style>