<template>
  <div class="hello">
  <div>
  <b-nav tabs>
    <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled>counter:{{numCorrect}}/{{numTotal}}</b-nav-item>
    <!-- <b-nav-item>Another Link</b-nav-item>
    <b-nav-item disabled>Disabled</b-nav-item> -->
  </b-nav>
</div>
  </div>
</template>

<script>
export default {
 
  props: 
[ 'numCorrect',
   'numTotal']
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
