<script setup lang="ts">
import type { Options, SubmitEvent, CartChangeEvent, CartClearEvent, SeatChangeEvent } from 'seatchart';
import SeatChart from './library/components/SeatChart.vue';
import 'seatchart/dist/seatchart.min.css';

const options: Options = {
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
    <SeatChart
        :options="options"
        @cart:submit="onSubmit"
        @update:cartChange="onCartChange"
        @update:cartClear="onCartClear"
        @update:seatChange="onSeatChange"
    />
    <h2>View the console to see events</h2>
  </div>
</template>

<style>
.economy {
  color: white;
  background-color: #43aa8b;
}

.first-class {
  color: white;
  background-color: #277da1;
}

.reduced {
  color: white;
  background-color: #f8961e;
}
</style>
