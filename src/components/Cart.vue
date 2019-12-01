<template>
	<div class="cart-content" v-show="showcartlist">
          <div class="shop-cart-content" >

             <CartSlot v-for="(cartval, cartind) in shoppingcart" :cartval="cartval" :key="cartval.id"  :cartind="cartind" @remove-Item="removeFromCart"/>
          </div>
          <div class="total-shop-cart">
            <div class="row">
              <div class="col-3">
                <button type="button" class="btn btn-sm btn-primary check-out-btn" id="CheckoutBtn" @click="checkCartOut">Checkout</button>
              </div>
              <div class="col-6"> </div>
              <div class="col-3">{{ totalprice | currencyfilter}} </div>
            </div>
          </div>
      </div>
</template>

<script>
import CartSlot from "@/components/CartSlot";

export default {
   components: {
      CartSlot
  },  
	props: ['shoppingcart', 'totalprice','showcartlist'],
	methods: {
		removeFromCart: function(cartind) {
      this.$emit('remove-Cart', cartind)
    },
    checkCartOut: function(){
      this.$emit('checkCartOut');
    }
	}
}
</script>
<style scoped>
.cart-content{
  position: fixed;
  right: 0em;    
  margin-top: 4px;
  background: rgba(0, 0, 0, 0.85);
  color: white;
  z-index: 1;
  width: 400px;
  padding:1rem;
  text-align:left;
}


.total-shop-cart{
  border-top:#ccc 2px solid;
  padding-top:1rem;
}
.shop-cart-content p {
  color:#aaa;
}

.cart-remove{
	width:80px;
	height:60px;
	z-index:100;
	position:absolute;
	top:0;	
	font-size:35px;
	text-align:center;
	color:red;
}
.check-out-btn {
  padding: 10px;
}
</style>
