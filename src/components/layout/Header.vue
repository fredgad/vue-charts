<template>
  <header class="header">
    <h1>TodoList</h1>
    <div id="nav">
      <router-link to="/home"
        >Характерристики мозга на разных этапах жизни человека</router-link
      >
      <router-link to="/about">Диаграмма</router-link>
      <router-link to="/scrollbarplugin"
        >Кастомная полоса прокрутки</router-link
      >
      <router-link to="/photo">Фоторез</router-link>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped lang="scss">
.header {
  background: #333;
  color: #fff;
  text-align: center;
  padding: 10px;

  #nav > * {
    border: 1px solid #eee;
    padding: 4px;
    margin: 20px;
    font-weight: 800;
  }
  #nav > *:hover {
    background: rgb(255, 94, 0);
  }

  a {
    color: #fff;
    padding-right: 5px;
  }
}
</style>
