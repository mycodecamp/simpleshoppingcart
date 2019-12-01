<template>
	
	<div class="row">
		<div class="col-3">
			<img :src="cartval.image" width="80px" height="60px" :alt="cartval.name" />
			<a href="#" class="cart-remove" @click="removeFromCart(cartind)">
				<font-awesome-icon icon="times" size="1x"/>
			</a>
		</div>
		<div class="col-6">
			{{cartval.name}}
			<p><small>{{cartval.color}}</small></p>
		</div>               
		<div class="col-3">{{cartval.price| currencyfilter}}</div>
	</div>
	
</template>

<script>

export default {
	props: ['cartval','cartind'],
	methods: {
		removeFromCart: function(cartind) {
           this.$emit('remove-Item', cartind)
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
</style>
