<template>
  
    <!-- As a heading -->
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 h1">Navbar</span>
        <div class="btn-group" role="group" aria-label="Basic radio toggle button group">
            <label class="btn btn-outline-primary" for="btnradio1">Bloques
            <input type="radio" class="btn-check" name="btnradio" id="btnradio1" autocomplete="off" checked>
            </label>
            
            <label class="btn btn-outline-primary" for="btnradio2">Python
            <input type="radio" class="btn-check" name="btnradio" id="btnradio2" autocomplete="off">
            </label>
            
          </div>
      </div>
    </nav>
    
</template>

<script>

export default {
  name: 'HeaderBar'
}
</script>