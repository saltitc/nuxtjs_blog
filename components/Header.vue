<template>
    <div class="container-fluid home-slider">
      <div id="carouselExampleCaptions" class="carousel slide" data-ride="carousel">
        <div class="carousel-inner">
          <div class="carousel-item active" style="background-color: #343a40!important">
            <div class="carousel-caption d-none d-md-block">
              <h1>
                {{ title }}
              </h1>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "Header",
    props: ['title']
}
</script>
  
  <style scoped>
  
  </style>