<template>
  <div class="order-system">
    <div class="order-system__controls">
      <h2>Controls</h2>
      <button class="order-system__control-btn" @click="addNormalOrder()">
        New Normal Order
      </button>
      <button class="order-system__control-btn" @click="addVIPOrder()">
        New VIP Order
      </button>
      <button class="order-system__control-btn" @click="addBot()">+ Bot</button>
      <button class="order-system__control-btn" @click="removeBot()">
        - Bot
      </button>
    </div>

    <div class="order-system__pending">
      <h2 class="mb-5">Pending Orders</h2>
      <!-- loop through array with v-for -->
      <h4 color="blue">Order 1</h4>
      <h4 color="blue">Order 2</h4>
      <h4 color="blue">Order 3</h4>
    </div>

    <div class="order-system__completed">
      <h2 class="mb-5">Completed Orders</h2>
      <!-- loop through array with v-for -->
      <h4 color="green">Order 1</h4>
      <h4 color="green">Order 2</h4>
      <h4 color="green">Order 3</h4>
    </div>

    <div class="order-system__bots">
      <h2>Available Bots</h2>
      <!-- loop through array with v-for -->
      <h4>Bot 1</h4>
      <h4>Bot 2</h4>
      <h4>Bot 3</h4>
    </div>
  </div>
</template>

<script setup></script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.order-system {
  display: flex;
  justify-content: space-evenly;

  &__controls {
    display: flex;
    flex-direction: column;
    margin: auto 0 auto 0;
  }

  &__control-btn {
    margin: 4px 0 0 0;
    padding: 5px;
  }

  &__bots {
    margin: auto 0 auto 0;
  }
}
</style>
