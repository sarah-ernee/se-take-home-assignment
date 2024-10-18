## Order Queue System

Simple ordering system with queueing of orders and bots that tend to the orders. Built with Vue3 Composition API.

Users are able to:
1. Add normal order
2. Add VIP order
3. Add bot
4. Remove bot
5. View queue of pending and completed orders
6. View queue of available bots

# How to Use

1. Clone the repository
2. Run `npm install` to install used dependencies and packages
3. Run application on localhost with `npm run serve` 

# Possible optimization

Further implementations could include:
1. Role-based access to limit certain actions: adding and removing bots, placing VIP orders
2. Deactivation of bot while it is processing should be prevented, only removed once its last order is completed
3. Limit number of VIP orders allowed at a time / bots dedicated to VIP orders only to prevent neglect of normal orders when there's too many VIP orders
4. Possible performance issues during high volume of orders
5. Better UI layout especially when order list grows long


