<template>
<div>
  <h1>Write Text Here!</h1>
  <form
    @submit.prevent="onSubmit"
  >
    <input
      v-model="thing"
      type="text"
      placeholder="Write here.." 
    />
    <button>
      Click
    </button>
  </form>
  <!-- {{ things }} -->
  <div 
    v-for="thing in things" 
    :key="thing.id" 
    class="card"
  >
    <div class="card-body">
      <input
        type = "checkbox"
        true-value = "Y"
        false-value = "N"
        v-model = "checkedValues"
      >
      {{ thing.text }}
    </div>
  </div>
  <button
    @click="isDelete"
  >
    Delete
  </button>
</div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const thing = ref("");
    const things = ref([]);
    const answer = ref(false);
    const checkedValues = ref("")

    // console.log(inputText)
    
    const onSubmit = () => {
      if(thing.value === ''){return}
      // 1. click하면 input에 입력한 값이 list에 담긴다.
      for(let i = 0; i < things.value.length; i++){
        if(things.value[i].text === thing.value){
          const answer = true;
          return answer.value;
        }
      }
      if(answer.value === false){
        things.value.push({
        id: thing.value,
        text: thing.value
      }); 
      thing.value='';
      } 
      else{
        console.log("중복");
      }
    }

    const isDelete = () => {
      let arr = []
      if (checkedValues.value === "N") {
        things.value.filter((item) => {
          arr = things.value.push(item)
          // return arr;
          console.log(arr);
          console.log(checkedValues.value)
        })
      }
      // console.log(checkedValues)
    }

    return {
      // things: [
      //   {text : "자고싶어", age:35},{text : "쉬고싶어",age:55},{text : "먹고싶어",age:5},{text : "놀고싶어",age:15},{text : "웃고싶어",age:25}
      // ],
      onSubmit,
      things,
      thing,
      isDelete,
      answer
    }
  },
}
</script>

<style>
  .card{
    width: 250px;
    height: 50px;
    border: 2px solid green;
    border-radius: 10px;
    line-height: 15px;
    margin: 10px 0;
  }
</style>