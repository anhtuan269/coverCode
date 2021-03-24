<template>
  <div class="product-category">
    <Category :categories="categories" :subCategory="subCategory">
    </Category>
    <Products :products="products" :gallery="gallery"/>
  </div>
</template>

<script>
import Category from "./components/Category.vue";
import Products from "./components/Products.vue";
export default {
  name: "App",
  components: {
    Category,
    Products,
  },
  data(){
    return{
      categories:[],
      subCategory:[],
      products:[],
      gallery:[]
    }
  },
  created(){
    this.fetchCategory();
    this.fetchProducts();
  },
  methods: {
    fetchCategory(){
      fetch("/categories.json")
      .then(res => res.json())
      .then(cate => {
        if(cate.status === 200){
          cate.result.map((c) =>{
            this.categories.push({
              id: c.id,
              name: c.name,
              url: c.url,
              img_ulr: c.image_url,
              sub: c.sub_category            
            });
            c.sub_category.map((sub) => {
              this.subCategory.push({
                id: sub.id,
                parent_id: sub.parent_id,
                name: sub.name,
                url: sub.url,

              })
            })
          })
        }
      })
      .catch(err => alert(err))
      console.log(this.categories);
      console.log(this.subCategory);
    },
    fetchProducts(){
      fetch("/products.json")
      .then(res => res.json())
      .then( product => {
        if(product.status ===200){
          product.result.map(p =>{
            this.products.push({
              id: p.id,
              name: p.name,
              url: p.url,
              img: p.default_image_url
            })
            p.gallery.map(g => {
              this.gallery.push({
                url: g.image_url,
                thumb: g.thumbnail_url,
                img: g.image
              });
            });
          });
        }
      })
    .catch(err => alert(err));
    console.log(this.products);
    console.log( this.gallery);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  font-size: 16px;
  color: #222;
  box-sizing: border-box;
}
.product-category{
  display: grid;
  grid-template-columns: 15% 75%;
  justify-content: center;
}
a {
  text-decoration: none;
  transition: all 0.3 linaer;
}
a:hover {
  color:greenyellow;
}
</style>
