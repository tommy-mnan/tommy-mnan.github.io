<template>

  <div  v-if="recipe.length != 0" class="small-con">
    <figure >
      <img :src="recipe.image_url" class="mainImage"/>
      <h1 class="recipe-title"><span>{{recipe.title}}</span></h1>
    </figure>
    <div class="recipe-ingredient">
        <ul>
            
            <li v-for="ingredient in recipe.ingredients.slice(from,to)">
                <i class="far fa-check-circle"></i>
                {{ingredient}}
            </li>
        </ul>
        
    </div>
    <div class="recipe-howto">
        <button class="btn-add-to-list btn peach-gradient btn-rounded btn-sm my-0 waves-effect waves-light" @click="sendShoppingList()">ADD TO LIST</button>
        <button class="btn peach-gradient btn-rounded btn-sm my-0 waves-effect waves-light" @click="howToCook()">How To Cook</button>
    </div>
    
  </div>
</template>

<script>
import { eventBus } from '../main';
export default {
    data(){
        return{
            recipeId : '',
            recipe : [],
            from : 0,
            to : 30
        }
    }, 
    
    methods:{
        fetchData() {
        console.log("masuk" + this.recipeId);
            this.$http.get('https://www.food2fork.com/api/get?key=1a3995484c34fb9593dc26d1b3cdb0b0&rId='+this.recipeId)
                    .then(response =>{
                    this.recipe = response.data.recipe;
                    this.checkRecipe();
                }, function(error){
                    console.log(error.statusText);
                });    
        
        },
        checkRecipe(){
            var n = this.recipe.ingredients.indexOf("_____");
            if(n > 0){
                this.to = n;
            }else{
                this.to = 30;
            }
            
        },
        howToCook(){
            window.open(this.recipe.source_url);
        },
        sendShoppingList(){
           eventBus.$emit('shoppingList',this.recipe.ingredients.slice(this.from,this.to));
        }
        

    },
    created() {
        eventBus.$on('receiptId', (event) =>{
            this.recipeId = event;
            this.fetchData();
            
        });
    },
    mounted(){
        
    }
};
</script>
<style lang="scss">

.small-con{
    min-height: 41rem;
}

.mainImage{
    width: 100%;
    display: block;
    height: 100%;
    object-fit: cover;
}

figure {
    height: 17rem;
    position: relative;
    transform: scale(1.04) translateY(-1px);
    transform-origin: top;
    margin-bottom: 0px;
}

figure::before{
    content: '';
    display: block;
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background-image: linear-gradient(to right bottom,#F59A83, #FBDB89);
    opacity: .6;
}

.recipe-title{
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translate(-50%, 20%) skewY(-6deg);
    color: #fff;
    font-weight: 700;
    font-size: 1.5rem;
    text-transform: uppercase;
    width: 70%;
    line-height: 1.95;
    text-align: center;
}

.recipe-title span {
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;
    padding: 1rem 2rem;
    background-image: linear-gradient(to right bottom, #F59A83, #FBDB89);
}

.recipe-ingredient{
    background-color: #F9F5F3;
    padding: 5rem 2rem 2rem 2rem;
    width: 100%;
    min-height: 20rem;

}

ul {
  -webkit-columns: 2;
     -moz-columns: 2;
          columns: 2;
    padding-left: 0;
    padding-top: 3%;
    font-size: 0.8rem;
    text-overflow:ellipsis; 
    text-transform: uppercase;
    color : #F59A83;
    font-weight: 400;
    list-style-type :none;
}

ul li {
  list-style-position: inside;
  -webkit-column-break-inside: avoid;
            page-break-inside: avoid;
                 break-inside: avoid;
    text-indent:-10px; 
    margin-left:20px;
}

.recipe-howto{
    padding : 1rem 2rem 2rem 2rem;
    text-align: center;
    background: #F9F5F3;
}
</style>

