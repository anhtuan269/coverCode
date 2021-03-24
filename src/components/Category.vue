<template>
  <div class="category">
    <ul class="menu">
      <li><h3>Categories</h3></li>
      <li
        v-for="(cat, index) in categories"
        :key="index"
        :id="cat.id"
      >
        <a
          href="#"
          target="_blanck"
          @click.prevent="addClass(index)"
          :class="{actived: actived}"
        >
        {{cat.name}}
          <ul v-if="cat_selected == cat.id"  class="sub_menu" style="margin-left: 20px;">
            <li v-for="( scat, i ) in cat.sub" :key="i">
              <a :href="scat.url"> {{scat.name}}</a>
            </li>
          </ul>
        </a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      active: "",
      actived: false,
      cat_selected:'',
      sub_menu: "sub-menu"
    };
  },
  props: {
    categories: Array,
    subCategory: Array,
  },
  watch: {},
  methods: {
    addClass(index) {
      this.cat_selected = this.categories[index].id;
      this.actived = !this.actived;
      console.log(this.active);
    },
  },
};
</script>
<style scoped>
.category .menu .sub-menu li {
  margin-left: 15px;
  display: none;
}
/* .category li  .sub-menu {
    display: none;
} */

.category .menu  li a.actived  ul {
  display: block;
}
.category .menu  li a  ul {
 display: none;
}

ul {
  text-align: left;
  padding: 10px 0px;
}
ul li {
  list-style: none;
  padding: 10px 0;
}
a:hover {
  color: greenyellow;
}
</style>
