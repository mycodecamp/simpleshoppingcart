<template>
 
    <nav class="site-header sticky-top py-1 ">
      <div class="container d-flex flex-column flex-sm-row justify-content-between">
        
        <span class="py-2">Simple Shopping Cart</span>        
        
        <a class="py-2 d-md-inline-block" href="#" v-on="cartcounter > 0 ? {click: () => toggleCart()} : { click: ($event) => $event.preventDefault() } ">
          <font-awesome-layers class="fa-layers fa-fw">
            <font-awesome-icon icon="shopping-cart" size="1x"/>
            <font-awesome-layers-text class="text-white fa-layers-counter custom-layer-counter" transform=" up-0 right-23" :value="cartcounter"/>
          </font-awesome-layers>
        </a>
      </div>

      <Cart :showcartlist="showcartlist"  :shoppingcart="shoppingcart" :totalprice="totalprice" @remove-Cart="removeItem" @checkCartOut="checkCartOut"/>
    </nav>
</template>

<script>

import Cart from "@/components/Cart";

export default {
  components: {
      Cart
  },  
  props: ['cartcounter', 'shoppingcart', 'totalprice'],
  data () {
        return {
            showcartlist: false,            
        }
            
    },
    methods: {
         toggleCart: function() {
           this.showcartlist = !this.showcartlist;
        },
        removeItem: function(cartind) {

           this.$emit('remove-Cart', cartind)
        },
        checkCartOut: function() {

           this.$emit('checkCartOut')
        }
     
    },
    watch:{
      cartcounter: function(){
        if(this.cartcounter <= 0) this.toggleCart();
        
      }
    }
 }
</script>
<style>
.site-header {
  background-color: rgba(0, 0, 0, .85);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  backdrop-filter: saturate(180%) blur(20px);
}
.site-header a, .site-header span {
  color: #ccc;
}

.site-header a:hover {
  color: #fff;
  text-decoration: none;
}
.custom-layer-counter {
  overflow: visible;
  width: fit-content;
}


</style>
