<template>
    <div class="main-page">
        <div class="left-menu">
            左
        </div>
        <div class="right-menu">
            右
        </div>
    </div>
</template>

<style scoped lang="scss">
.main-page {
  display: flex;
  height: calc(100vh - 60px);
  .left-menu {
    width: 350px;
    background-color: #f7f6f3;
  }
  .right-view {
    flex-grow: 1;
    padding: 10px;
  }
}
</style>
