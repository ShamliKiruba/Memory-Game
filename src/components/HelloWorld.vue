/* eslint-disable */
<template>
<div>
  <h1>Image Flip with Text</h1>
  <h3>Hover over the image below:</h3>
  <button @click="checkGenerated()">Check again</button>
  <table>
    <thead></thead>
    <tbody>
      <tr v-for="(asd,index) in array" :key="index">
        <td v-for="(item,index) in asd" :key="index">
          <div class="flip-box">
            <div class="flip-box-inner">
              <div class="flip-box-front">
                <img src="img_paris.jpg" alt="Paris" style="width:100px;height:100px">
              </div>
              <div class="flip-box-back">
                <img :src="item" alt="Paris" style="width:100px;height:100px">
              </div>
            </div>
          </div>
        </td>
      </tr>
    </tbody>
  </table> 
</div>
</template>
<script>
export default {
  data() {
    return {
      row:4,
      coln:4,
      number : [],
      temp : ['http://www.everlastingcelebrations.com/wp-content/uploads/2018/09/Top-Ganesh-Chaturthi-Messages-Images-Photos.jpg','https://imgd.aeplcdn.com/1280x720/bw/models/yamaha-r15.jpg?20191001112540&q=80',
      'https://media.istockphoto.com/photos/tomato-isolated-on-white-background-picture-id466175630?k=6&m=466175630&s=612x612&w=0&h=fu_mQBjGJZIliOWwCR0Vf2myRvKWyQDsymxEIi8tZ38=',
      'https://images.all-free-download.com/images/graphiclarge/daisy_pollen_flower_220533.jpg','https://image.shutterstock.com/image-vector/smiley-vector-happy-face-260nw-408014413.jpg','https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png',
      'https://image.shutterstock.com/image-vector/cartoon-heart-vector-260nw-237494677.jpg',
      'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQn5MXPV60GzTqGjish0u84lTuPEhTkTnrSV2ML3E359n7_0RkQ_g']
    }
  },
  methods: {
    createArray() { /* eslint-disable */
      let itemCount = (this.row * this.coln)/2; //8
      let array = [[]];
      let generated = [], obj = {};
      for(let i=0;i< this.row;i++) {
        array.push([]);
        for(let j=0;j< this.coln;j++) {
          let item = this.number[Math.floor(Math.random()*this.number.length)];
          if(obj[item] <= 2) {
            obj[item]++;
          } else {
            obj[item] = 1;
          }
          if(obj[item] == 2) {
            let index = this.number.indexOf(item);
            this.number.splice(index, 1);
          }
          if(obj[item] <= 2) {
            array[i][j] = this.temp[item]; 
            generated.push(item);
          }
        }
      }
      console.log('obj: ', obj);
      console.log('generated: ', generated);      
      console.log('array: ', array);
      this.array = array;
    },
    checkGenerated() {
      for(let i =0;i < this.temp.length; i++) {
        this.number.push(i);
      }
      this.createArray();
    }
  },
  created() {
    this.checkGenerated();
  }
}
</script>
<style>
body {
  font-family: Arial, Helvetica, sans-serif;
}

.flip-box {
  background-color: transparent;
  width: 100px;
  height: 100px;
  border: 1px solid #f1f1f1;
  perspective: 500px;
}

.flip-box-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-box .flip-box-inner {
  transform: rotateY(180deg);
}

.flip-box-front, .flip-box-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.flip-box-front {
  background-color: #bbb;
  color: black;
}

.flip-box-back {
  background-color: #555;
  color: white;
  transform: rotateY(180deg);
}
</style>
