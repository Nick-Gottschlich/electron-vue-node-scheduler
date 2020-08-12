<template>
  <div>
    <b-time
      v-model="value"
      locale="en"
      @context="onContext"
    ></b-time>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
// eslint-disable-next-line @typescript-eslint/ban-ts-ignore
// @ts-ignore
import schedule from 'node-schedule';

@Component
export default class HelloWorld extends Vue {
  value = '';

  // eslint-disable-next-line @typescript-eslint/no-empty-function
  scheduleJob = schedule.scheduleJob('* * * * *', () => {});

  // eslint-disable-next-line class-methods-use-this
  onContext(context) {
    // get hours and minutes off of something like '19:12:00'
    const hours = context.value.split(':')[0];
    const minutes = context.value.split(':')[1];

    this.scheduleJob.cancel();
    this.scheduleJob = schedule.scheduleJob(
      `${minutes || '00'} ${hours || '00'} * * *`,
      () => {
        console.log('job ran on schedule!');
      },
    );
  }

  data() {
    return {
      value: this.value,
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
