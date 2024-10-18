<template>
  <div class="order-system">
    <div class="order-system__controls">
      <h2>Controls</h2>
      <button class="order-system__control-btn" @click="addOrder('normal')">
        New Normal Order
      </button>
      <button class="order-system__control-btn" @click="addOrder('vip')">
        New VIP Order
      </button>
      <button class="order-system__control-btn" @click="addBot">Add Bot</button>
      <button class="order-system__control-btn" @click="removeBot">
        Remove Bot
      </button>
    </div>

    <div class="order-system__pending">
      <h2 class="mb-5">Pending Orders</h2>

      <div v-if="pendingOrderCount > 0">
        <h4 v-for="order in pendingOrders" :key="order.id">
          Order #{{ order.id }} ({{ order.type }}) -
          {{ order.processing ? "Processing" : "In Queue" }}
        </h4>
      </div>
    </div>

    <div class="order-system__completed">
      <h2 class="mb-5">Completed Orders</h2>

      <div v-if="completedOrderCount > 0">
        <h4 v-for="order in completedOrders" :key="order.id">
          Order #{{ order.id }} ({{ order.type }})
        </h4>
      </div>
    </div>

    <div class="order-system__bots">
      <h2>Available Bots</h2>

      <div v-if="activeBotCount > 0">
        <div v-for="bot in activeBots" :key="bot.id">
          <h4>
            Bot #{{ bot.id }} -
            <span
              :style="{ color: bot.status === 'active' ? 'orange' : 'black' }"
            >
              {{ bot.status }}
            </span>
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

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

  if (type === "vip") {
    const lastVIPIndex = pendingOrders.value.findLastIndex(
      (order) => order.type === "vip"
    );
    pendingOrders.value.splice(lastVIPIndex + 1, 0, newOrder);
  } else {
    pendingOrders.value.push(newOrder);
  }

  processOrders();
};

const addBot = () => {
  activeBots.value.push({
    id: ++botCounter.value,
    status: "idle",
  });
  processOrders();
};

const removeBot = () => {
  if (activeBots.value.length === 0) return;

  const removedBot = activeBots.value.pop();
  if (removedBot.status === "active") {
    const processingOrder = pendingOrders.value.find(
      (order) => order.processing
    );
    if (processingOrder) processingOrder.processing = false;
  }
  processOrders();
};

const processOrders = () => {
  const idleBots = activeBots.value.filter((bot) => bot.status === "idle");
  const availableOrders = pendingOrders.value.filter(
    (order) => !order.processing
  );

  idleBots.forEach((bot) => {
    if (availableOrders.length > 0) {
      const order = availableOrders.shift();
      bot.status = "active";
      order.processing = true;

      setTimeout(() => {
        pendingOrders.value = pendingOrders.value.filter(
          (item) => item.id !== order.id
        );
        completedOrders.value.push(order);
        bot.status = "idle";
        processOrders();
      }, 10000);
    }
  });
};

// Array length properties
const pendingOrderCount = computed(() => pendingOrders.value.length);
const completedOrderCount = computed(() => completedOrders.value.length);
const activeBotCount = computed(() => activeBots.value.length);
</script>

<style lang="scss">
.order-system {
  display: flex;
  justify-content: space-evenly;

  &__controls {
    display: flex;
    flex-direction: column;
    margin: auto 0;
  }

  &__control-btn {
    margin: 4px 0 0 0;
    padding: 5px;
  }

  &__bots {
    margin: auto 0;
  }
}
</style>
