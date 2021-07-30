<template>
  <!-- Center - Moves text to center. p-4 adds padding on all sides, mb-10 add a margin to push it down. -->
  <header class="text-center bg-blue-800 
  text-white
  p-4 
  mb-10">
    <!-- md means when we hit a medium breakpoint, the text will get bigger. -->
    <div class="text-3xl md:text-5xl font-bold mb-3">
      <i class="fa fa-viruses"></i>  
      Covid-19 Tracker
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header'
}
</script>
