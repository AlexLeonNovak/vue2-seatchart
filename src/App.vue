<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import type { Options, SubmitEvent, CartChangeEvent, CartClearEvent, SeatChangeEvent } from 'seatchart';
import SeatChart from './library/components/SeatChart.vue';

const options: Options = {
  cart: { visible: false },
  legendVisible: false,
  map: {
    rows: 10,
    columns: 10,
    seatTypes: {
      default: {
        label: 'Economy',
        cssClass: 'economy',
        price: 15,
      },
      first: {
        label: 'First Class',
        cssClass: 'first-class',
        price: 25,
        seatRows: [0, 1, 2],
      },
      reduced: {
        label: 'Reduced',
        cssClass: 'reduced',
        price: 10,
        seatRows: [7, 8, 9],
      },
    },
    disabledSeats: [
      { row: 0, col: 0 },
      { row: 0, col: 9 },
    ],
    reservedSeats: [
      { row: 0, col: 3 },
      { row: 0, col: 4 },
    ],
    selectedSeats: [
      { row: 0, col: 5 },
      { row: 0, col: 6 },
    ],
    rowSpacers: [3, 7],
    columnSpacers: [5],
  },
};
const onSubmit = (e: SubmitEvent) => {
  console.log('SubmitEvent', e);
  alert(JSON.stringify(e, null, 4));
};
const onCartChange = (e: CartChangeEvent) => console.log('CartChangeEvent', e);
const onCartClear = (e: CartClearEvent) => console.log('CartClearEvent', e);
const onSeatChange = (e: SeatChangeEvent) => console.log('SeatChangeEvent', e);

</script>

<template>
  <div id="app">
    <header>
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

      <div class="wrapper">
        <HelloWorld msg="You did it!" />

        <nav>
          <router-link to="/">Home</router-link>
          <router-link to="/about">About</router-link>
        </nav>

        <SeatChart
            :options="options"
            @cart:submit="onSubmit"
            @update:cartChange="onCartChange"
            @update:cartClear="onCartClear"
            @update:seatChange="onSeatChange"
        />

      </div>
    </header>

    <router-view />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
