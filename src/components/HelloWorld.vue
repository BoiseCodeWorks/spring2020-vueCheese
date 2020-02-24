<template>
  <div class="hello">
    <img
      @click="mine"
      alt="Vue logo"
      src="https://nineplanets.org/wp-content/uploads/2019/09/moon.png"
    />
    <h3 :class="{ 'text-danger': cheese > 100 }">Count: {{ cheese }}</h3>
    <!-- <button v-if="count > 9" @click="buyPick">Buy Pick</button> -->
    <button
      class="btn btn-warning"
      v-for="equip in equipment"
      :key="equip.id"
      :disabled="cheese < equip.cost"
      @click="buy(equip)"
    >
      Buy {{ equip.name }} (owned: {{ equip.count }})
    </button>
    <button @click="cheese = 0">Reset</button>
  </div>
</template>

<script>
export default {
  name: "MoonComponent",
  mounted() {
    setInterval(() => {
      this.automine();
    }, 3000);
  },
  data() {
    return {
      cheese: 0,
      equipment: {
        picks: {
          id: 1,
          name: "pick",
          count: 0,
          cost: 10
        },
        carts: {
          id: 2,
          name: "carts",
          count: 0,
          cost: 25
        },
        moustrounauts: {
          id: 3,
          name: "mouse",
          count: 0,
          cost: 100
        }
      }
    };
  },
  methods: {
    mine() {
      let picks = this.equipment.picks.count;
      let carts = this.equipment.carts.count * 5;
      let mouses = this.equipment.moustrounauts.count * 10;
      this.cheese += 1 + picks + carts + mouses;
    },
    automine() {
      this.cheese++;
    },
    buy(equip) {
      if (equip.cost < this.cheese) {
        this.cheese -= equip.cost;
        equip.count++;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
