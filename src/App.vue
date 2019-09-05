<template>
<div class="container">
  <app-search-bar @searchList="datas = $event"></app-search-bar>
   <div class="row">
    <div class="col-sm col-sm-3">
     <app-recipes-list :datas="datas"></app-recipes-list>
    </div>
    <div class="col-sm col-sm-6 middle-col">
      <app-recipe-details></app-recipe-details>
      
    </div>
    <div class="col-sm" col-sm-3>
      <app-shopping-list></app-shopping-list>
    </div>

  
  </div>
</div>
</template>

<script>
  import SearchBar from './components/SearchBar.vue';
  import RecipestList from './components/RecipesList.vue';
  import RecipeDetails from './components/RecipeDetails.vue';
  import ShoppingList from './components/ShoppingList.vue';
  export default {
    components: {
      'app-search-bar' : SearchBar,
      'app-recipes-list' : RecipestList,
      'app-recipe-details' : RecipeDetails,
      'app-shopping-list' : ShoppingList
    },
    data () {
      return {
        datas: []
      }
    },
    methods:{
      newdata(event){
        console.log(event);
      }
    }  
    
  }
</script>

<style lang="scss">
.container{
  background-color: #F9F5F3;
  padding-left :5px;
  padding-right :5px;
  margin-bottom: 5rem;
}
.col-sm{
  min-height: 35rem;
  margin: 1px;
  padding-right : 0px;
}
.middle-col{
  background-color: white;
  padding-left: 10px;
  padding-right: 10px;

}
.row{
  margin-top: 0px;
}
</style>
