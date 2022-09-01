<template>
    <header class="header">
        <h1>Задачи</h1>
        <div class="add_task" @click='$emit("showDialog", header)'>
          <div class="bar horizontal"></div>
          <div class="bar vertical"></div>
        </div>
    </header>
</template>

<script>
    export default {
       
    }
</script>

<style  scoped>
h1 {
  margin-left: 40px;
}

.header {
  display: flex;
  justify-content: space-between;

}
.add_task {
  border-radius: 50%;
  width: 40px;
  height: 40px;
  background-color: #D6DBEB;
  position: relative;
  cursor: pointer;
}

.bar {
  top: 25%;
  left: 48%;
  position: absolute;
  background-color: #fff;
}

.horizontal {
  width: 2px;
  height: 20px;
  transform: rotate(90deg);
  background-color: #314B99;
}

.vertical {
  width: 2px;
  height: 20px;
  background-color: #314B99;
}
</style>