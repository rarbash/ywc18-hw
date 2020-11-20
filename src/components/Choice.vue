<template>
  <div>
    <div class="form-check card boxchecklist">
      <div class="list">
        <h6><strong>ประเภทร้านอาหาร</strong></h6>
        <div>
          <input type="radio" value="ทั้งหมด" v-model="checkedCategoryName" />
          <label class="form-check-label ml" for="exampleRadios1">
            ทั้งหมด
          </label>
        </div>
        <div v-for="(category, index) in categoriesLists" :key="index">
          <div>
            <input
              type="radio"
              :value="category.name"
              v-model="checkedCategoryName"
            />
            <label class="form-check-label ml" for="exampleRadios1">
              {{ category.name }}
            </label>
          </div>
        </div>
      </div>

      <div class="list">
        <h6><strong>จังหวัด/ใกล้ฉัน</strong></h6>
        <Dropdown :infoLists="provincesLists" />
      </div>

      <div class="list">
        <h6><strong>ราคา</strong></h6>
        <Dropdown :infoLists="priceRangeLists" />
      </div>

      <div class="list">
        <h6><strong>ประเภทร้านอาหารและเครื่องดื่ม</strong></h6>
        <div>
          <input
            type="radio"
            name="exampleRadios"
            id="exampleRadios1"
            value="ทั้งหมด"
            v-model="checkedSubcategoryName"
          />
          <label class="form-check-label ml" for="exampleRadios1">
            ทั้งหมด
          </label>
        </div>
        <div v-for="(subcategory, index) in selectedSubcategory" :key="index">
          <input
            type="radio"
            name="exampleRadios"
            id="exampleRadios1"
            :value="subcategory"
            v-model="checkedSubcategoryName"
          />
          <label class="form-check-label ml" for="exampleRadios1">
            {{ subcategory }}
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Dropdown from "@/components/Dropdown.vue";
export default {
  components: {
    Dropdown,
  },
  props: {
    categoriesLists: Array,
    provincesLists: Array,
    priceRangeLists: Array,
  },
  computed: {
    selectedSubcategory() {
      const subIndex = this.categoriesLists.findIndex(
        (item) => item.name === this.checkedCategoryName
      );
      return this.checkedCategoryName !== "ทั้งหมด"
        ? this.categoriesLists[subIndex].subcategories
        : this.allSubCategory;
    },
  },
  watch: {
    checkedCategoryName() {
      this.$emit("onCheckedCategoryChange", this.checkedCategoryName);
    },
    checkedSubcategoryName() {
      this.$emit("onCheckedSubcategoryChange", this.checkedSubcategoryName);
    },
  },
  data() {
    return {
      checkedCategoryName: "ทั้งหมด",
      checkedSubcategoryName: "ทั้งหมด",
      allSubCategory: [],
    };
  },
  mounted() {
    for (const index in this.categoriesLists) {
      this.allSubCategory.push(...this.categoriesLists[index].subcategories);
    }
  },
};
</script>

<style>
.boxchecklist {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  max-height: 100%;
  padding-left: 0.5rem;
}
.list {
  margin: 10px;
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.ml {
  margin-left: 1rem;
}
</style>