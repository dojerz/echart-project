<script setup>
import { onMounted, reactive } from 'vue'
import * as echarts from 'echarts';
import axios from 'axios';

defineProps({
  msg: {
    type: String,
    required: true
  }
})


const testdata = reactive({ val: null });
let data = reactive([]);
let option = reactive({
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      type: 'line',
      data: data
    }
  ]
});

onMounted(/*() => {

  let chartDom = document.getElementById('chart');
  let mc = echarts.init(chartDom);


  data.push(7);
  data.push(6);
  data.push(5);
  data.push(4);
  data.push(4);
  data.push(3);
  data.push(1);

  mc.setOption(option);

  console.log(main.value);
  console.log(mc);

},*/
  async () => {
    let chartDom = document.getElementById('chart');
    let mc = echarts.init(chartDom);


    data.push(7);
    data.push(6);
    data.push(5);
    data.push(4);
    data.push(4);
    data.push(3);
    data.push(1);

    mc.setOption(option);

  console.log(mc);

  const resp = await axios.get('http://localhost:5030/weatherforecast');
  console.log(resp);
  /*
    const resp = await fetch(
      'http://localhost:5030/weatherforecast',
      {
        method: 'GET',
        mode: "no-cors"
      }
    )
    testdata.val = (await resp).json();*/
  }
)

</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <div id="chart" style="width: 600px;height:400px;"></div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
