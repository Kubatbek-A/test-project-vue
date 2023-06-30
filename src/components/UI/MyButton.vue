<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script></script>

<style>
.btn {
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
  cursor: pointer;
}

.btn:hover {
  background-color: rgb(0, 128, 128, 0.1);
}
</style>
