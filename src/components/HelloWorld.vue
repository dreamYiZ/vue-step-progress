<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    
    <step-progress :steps="['吃饭','拉屎','吃面', '睡觉']" :activeStep="0" />
    <step-progress :steps="['吃饭','拉屎','吃面', '睡觉']" :activeStep="1" />
    <step-progress :steps="['吃饭','拉屎','吃面', '睡觉']" :activeStep="2" />
    <step-progress :steps="['吃饭','拉屎','吃面', '睡觉']" :activeStep="tabIndex" @change="tabOnChange" />

  </div>
</template>

<script>
import StepProgress from './StepProgress'; 
import RLog from 'rentoo';

export default {
  name: 'HelloWorld',
  data(){
    return {
      tabIndex: 3
    }
  },
  components: {
    'step-progress': StepProgress
  },
  props: {
    msg: String
  },
  methods: {
    tabOnChange(e){
      RLog('tabOnChange:'+ e);
      this.tabIndex = e;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
