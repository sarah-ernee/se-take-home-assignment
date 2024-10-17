<template>
  <div class="order-system">
    <div class="order-system__controls">
      <h2>Controls</h2>
      <button
        class="order-system__control-btn"
        @click="() => addOrder('Normal')"
      >
        New Normal Order
      </button>
      <button class="order-system__control-btn" @click="() => addOrder('VIP')">
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

<script setup>
import { ref } from "vue";

const orderCounter = ref(0);
const botCounter = ref(0);
const pendingOrders = ref([]);
const completedOrders = ref([]);
const activeBots = ref([]);

const addOrder = (type) => {
  const newOrder = {
    id: ++orderCounter.value,
    type,
    processing: false,
  };

  if (type == "VIP") {
    console.log("bump up the queue");
  } else {
    pendingOrders.value.push(newOrder);
  }
};

const addBot = () => {
  activeBots.value.push({
    id: ++botCounter.value,
    status: 'Idle'
  })
}
</script>

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
