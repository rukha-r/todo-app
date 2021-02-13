<template>
  <div id="app">
    
    <TodoApp/>
    

  </div>
</template>


<script>
import TodoApp from './components/TodoApp';

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>


<style lang="scss">

body {
	background-color: gray;
	#app {
	margin-top: 100px;
	display: flex;
	justify-content: center;
	align-items: center;

}
}


</style>
