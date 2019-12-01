<template>
  
  <div class="col-md-4">
    <div class="card mb-4 shadow-sm">
        <slot name="image"></slot>
        <div class="card-body">
            
            <div class="d-flex justify-content-between align-items-center">
              <span class="card-text"><slot name="name"></slot></span>
                <span class="card-price"><slot name="price"></slot></span>                
            </div>
           
            <ColorList>
                <template v-slot:colorslist><slot name="laptopcolors"></slot></template>
            </ColorList>
            
            <div class="d-flex justify-content-end align-items-center">
             
              <slot name="addToCartBtnSlot"></slot>
              
            </div>

             
        </div>
       
    </div>
   
  </div>        
</template>

<script>
import ColorList from "@/components/ColorList";

export default {
    name: 'ProductList',
    components: {
      ColorList
    }
  
}
</script>


<style scoped>

.bd-placeholder-img {
        font-size: 1.125rem;
        text-anchor: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
      }

      @media (min-width: 768px) {
        .bd-placeholder-img-lg {
          font-size: 3.5rem;
        }
      }




.card-text {
  font-weight: 700;

}

.card-content {
  margin-top:10px;
  padding:10px;
  height:300px;
  overflow-y:scroll;
}

.card-price {
  font-weight: 700;
  color: #8a8a8a;
}
.add-to-cart{
   padding:10px;
}

.showdetail{
  padding:2px 10px;
  font-weight: 700;
  font-size:25px;
}
</style>
