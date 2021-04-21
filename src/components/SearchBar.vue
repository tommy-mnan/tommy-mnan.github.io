<template>
    <!--Navbar-->
    <nav class="navbar navbar-expand-lg navbar-dark pink lighten-3">
      <!-- Collapsible content -->
      <div class="navbar-collapse" id="navbarSupportedContent">
        <!-- Search form -->
        <div class="form-inline">
          <div class="md-form my-0" >
            <input
              class="form-control"
              :class="showUp"
              type="text"
              placeholder="Search"
              aria-label="Search"
              @keypress="search($event)"
              v-model="searchData"
            />
            <i class="fas fa-search text-white ml-3" :class="hide" aria-hidden="true" @click="showSearch()"></i>
          </div>
         </div>
      </div>
      <!-- Collapsible content -->

      <!-- Navbar brand -->
      <a class="navbar-brand" href="#">foodrecipe</a>
      
    </nav>
    <!--/.Navbar-->
</template>

<script>
    export default{
        data() {
            return{
                searchData: '',
                searcList: [],
                showUp: '',
                hide: ''
            }
        },
        methods : {
        search(event) {
        if (event.charCode === 13){
            this.fetchData();
        }
        },
        showSearch(){
          if(window.innerWidth <= 600){
            this.showUp = "showUp";
            this.hide = "form-control";
          }
          
        },
        fetchData() {
        this.$http.get('https://recipesapi.herokuapp.com/api/v2/recipes?q='+this.searchData+'&page=1')
                    .then(response =>{
                    this.searcList = response.data;
                    // console.log(this.searcList);
                    this.$emit("searchList",this.searcList);
                    this.searchData = '';
                }, function(error){
                    console.log(error.statusText);
                });
        },
        handleResize(){
            this.showUp = '';
            this.hide = '';
        }
    },
    created(){
      window.addEventListener('resize', this.handleResize)
      this.handleResize();
    } 

    }
</script>

<style lang="scss">
.pink{
     background-image: linear-gradient(to right bottom, #F59A83, rgb(231, 149, 128));
     height: 3.3rem; 

}
.navbar-brand {
  font-family: "Black Ops One", cursive;
}
.form-control{
    color: white;
}

.md-form{
      transition: width 2s;
}

@-webkit-keyframes fadeIn {
    from { opacity: 0; }
      to { opacity: 1; }
}  
@keyframes fadeIn {
    from { opacity: 0; }
      to { opacity: 1; }
}

@media screen and (max-width: 600px) {
  .form-control {
    display: none;
  }

  .showUp{
    display:inline;
    position: relative;
    top: -7px;
    -webkit-animation: fadeIn 1s;
    animation: fadeIn 1s;
  }

  .navbar-brand{
    position: absolute;
    right: 0;
  
  }

  .fa-search{
    cursor: pointer;
  }

  
}

</style>
