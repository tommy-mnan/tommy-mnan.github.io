<template>
    <div>
        <h5 class="sub-menu-title">MY SHOPPING LIST</h5>
        <div class="item-list" v-if="shoppingList.length > 0">
            <li v-for="item in shoppingList">{{item}}</li>
            
        </div>
        <div class="about">© by Tommy Meinando Powered by <br> <a href="https://www.food2fork.com" target="_blank">Food2Fork.com.</a></div>
    </div>
</template>

<script>
    import { eventBus } from '../main';
    export default{ 
        data() {
            return{
                shoppingList :[]
            }
        },
        mounted() {
            eventBus.$on('shoppingList', (event) =>{
                this.shoppingList.push.apply(this.shoppingList, event);
                
            });
        }
      
    }
</script>

<style lang="scss">
.sub-menu-title{
    color : #F59A83;
    padding: 1rem 1rem;
    text-decoration: underline;
    font-weight: 400;
    
}
.about{
    position:absolute;
    bottom:0;
    left:0;
    font-size: 0.6rem;
    padding: 1rem;
    color: dimgrey;
}

.about a{
    color: dimgrey;
}

.item-list{
   padding-left: 0.5rem;
   overflow:scroll;
   max-width: 90%;
   max-height:34rem; 
}

.item-list li{
    padding-left: 0;
    padding-top: 3%;
    font-size: 0.8rem;
    text-overflow:ellipsis; 
    text-transform: uppercase;
    color : #F59A83;
    font-weight: 400;
}
</style>
