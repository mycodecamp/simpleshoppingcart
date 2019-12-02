<template>
  
  <div v-bind:class="[(showdetail==false)? divClass : divClass2 ]">
    
      <div class="card mb-4 shadow-sm" v-bind:class="[(showdetail==true) ? divClass4:'']"> 
        <div v-bind:class="[(showdetail==true)? divClass : '', (showdetail==true)? divClass3 : '' ]" >
          <slot name="image"></slot>
          <div class="card-body">            
            <div class="d-flex justify-content-between align-items-center">
              <span class="card-text"><slot name="name"></slot></span>
                <span class="card-price"><slot name="price"></slot></span>                
            </div>
           
            <ColorList>
                <template v-slot:colorslist><slot name="laptopcolors"></slot></template>
            </ColorList>
          </div>
            
          <div class="d-flex justify-content-between align-items-center paddingadd">
            <button type="button" class="btn btn-sm btn-outline-primary showdetail" @click="toggleDetail">+</button>
            <slot name="addToCartBtnSlot"></slot>              
          </div>     
        </div>  
        <div class="card-content" v-show="showdetail" v-bind:class="[(showdetail==true)? cardContentClass : '' ]">
          <slot name="detail"></slot>
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
  },  
  data () {
    return {
      showdetail: false, 
      divClass: 'col-md-4',
      cardContentClass: 'col-md-8',
      divClass2: 'col-md-12',
      divClass3: 'paddingzero',
      rowClass:'row',
      divClass4:'changeCardDirection'   
    }            
  },
  methods: {
    toggleDetail: function() {
      this.showdetail = !this.showdetail;
    }     
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
 
  padding:20px 20px;
  text-align: justify;
  text-justify: inter-word;
  
}

.card-price {
  font-weight: 700;
  color: #8a8a8a;
}
.add-to-cart {
   padding:10px;
}

.paddingadd {
   padding:0 10px 10px;
}

.paddingzero {
  padding:0px!important;
}

.showdetail{
  padding:2px 10px;
  font-weight: 700;
  font-size:25px;
}

.changeCardDirection {
  flex-direction: row!important;

}
</style>
