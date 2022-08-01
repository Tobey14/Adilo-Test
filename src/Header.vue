<template>
  <header>
      <nav class="navbar sticky-top navbar-expand-lg navbar-light bg-light px-5">
          <a class="navbar-brand" href="#">
              <img src="./assets/images/swarm.svg" class="logo" alt="">
              <span class="ml-3 brandName">
                  Adilo
              </span> 
          </a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
        
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-5">
              <li class="nav-item">
                <a class="nav-link" href="#">Project <span class="sr-only">(current)</span></a>
              </li>

              <li class="nav-item dropdown active">
                  <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Tools & Apps
                    <i class="fa fa-angle-down mt-1"></i>
                  </a>
                  <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <a class="dropdown-item activate" href="#">SnapByte Recorder</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="#">AudioBounce</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="#">Sugar Voice</a>
                  </div>
              </li>
              <li class="nav-item">
                  <a class="nav-link" href="#">Channels</a>
              </li>
              
              <li class="nav-item">
                  <a class="nav-link disabled" href="#">Contacts</a>
              </li>


              <li class="nav-item">
                  <a class="nav-link" href="#">Analytics</a>
              </li>
              
              <li class="nav-item">
                  <a class="nav-link disabled" href="#">Settings</a>
              </li>
            </ul>

            <div class="form-inline ml-5 my-lg-0">
              <span class="help">Help</span>

              <img src="./assets/images/social-3.png" alt="" class="imageRight">

              <div class="mx-4 mt-1">
                  <span class="name mb-0 row">Cody Fisher</span>
                  <span class="mail row">cody@gmail.com</span>
              </div>
              


            </div>
          </div>
      </nav>
  </header>

</template>


<script>

export default {
  props: [], 
  data() {
    return {
     
    };
  },
  computed: {
    
  },
  methods: {
    
    
    
  },

  mounted() {

    

    
    

    
  },
};
</script>



<style scoped>



</style>