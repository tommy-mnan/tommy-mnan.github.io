<template>
  <div class="list-group">

    <a  href="#" 
        v-for="recipe in datas.recipes.slice(from, to)"
        class="list-group-item list-group-item-action" 
        v-if="datas.recipes.length != 0"
        @click="sendReceipId(recipe.recipe_id)">
        <img :src="recipe.image_url" class="mr-3"  />
        <div class="title-recipe">{{recipe.title}}</div>
        <p class="publisher">{{recipe.publisher}}</p>
    </a>
    <div class="paging">
        <i @click = "before()" class="far fa-arrow-alt-circle-left" v-if ="from >= 10" ></i>
        <i @click = "next()" class="far fa-arrow-alt-circle-right" v-if ="to < datas.count" ></i>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main';
export default {
    props:['datas'],
    data(){
        return{
            from : 0,
            to : 10
        }
    },
    methods:{
        sendReceipId(event){
           eventBus.$emit('receiptId',event);
        },
        next(){
            this.from = this.from + 10;
            this.to = this.to + 10;
        },
        before(){
            this.from = this.from - 10;
            this.to = this.to - 10;
        }

    }

};
</script>
<style lang="scss">

.mr-3{
    width: 3rem;
    height: 3rem;
    float: left;
    border-radius: 50%;
}

.title-recipe{
    padding-top: 3%;
    font-size: 0.7rem;
    overflow:hidden; 
    white-space:nowrap; 
    text-overflow:ellipsis; 
    text-transform: uppercase;
    color : #F59A83;
    font-weight: 400;
}
.publisher{
    font-size: 0.5rem;
    color: #968B87;
    text-transform: uppercase;
    font-weight: 600;
}
.list-group-item{
    padding-top: 5px;
    padding-bottom: 5px;
    border-radius: 5px;
}

.list-group-item:hover{
    background-image: linear-gradient(to right bottom, #F59A83, rgb(231, 149, 128));
    padding-left: 5px;
}

.list-group-item:hover .title-recipe{
    color : white;
}

.paging{
    font-size: 2rem;
    color : #F59A83;
    text-align: center;
}

.far{
    cursor: pointer;
}
</style>

