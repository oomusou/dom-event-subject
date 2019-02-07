<template>
  <div>
    <button v-stream:click="{ subject: click$, data: 2 }">+</button>
    <h1>{{ random$ }}</h1>
  </div>
</template>

<script>
import { map, startWith, scan, pluck } from 'rxjs/operators';

const subscriptions = function() {
  const random$ = this.click$.pipe(
    pluck('data'),
    startWith(0),
    scan((a, x) => a + x),
  );

  return {
    random$
  };
};

export default {
  name: 'HelloWorld',
  domStreams: ['click$'],
  subscriptions,
};
</script>
