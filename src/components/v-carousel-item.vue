<template>
  <div class="border">
    <div class="v-carousel-item">
      <img :src="require('../img/' + item_data.img)">
      <p>{{item_data.date}}</p>
      <div class="item_content">
        <div class="name">{{item_data.name}}</div>
        <div class="content">{{item_data.content}}</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'v-carousel-Item',
  components: {
  },
  props: {
    item_data: {
      type: Object,
      default: () => {}
    },
    imgSlide: {
      type: Boolean,
      default: true
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
.border{
  width: 260px;
  text-align: center;
  margin-right: 40px;
  padding: 20px; /* Поля */
  border: 1px solid #C8D9FB;
  -moz-box-sizing: border-box; 
  box-sizing: border-box;
}
.border:hover{
  border: 1px solid #527CCD;
}
.item_content {
  text-align: left;
  display: flex;
  flex-direction: column;
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-template-rows: repeat(2, 110px);
}
p {
  text-align: left;
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 22px;
  color: #527CCD;
  padding: none;
  margin: 10px 0 5px;
}
.name{
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 600;
  font-size: 16px;
  line-height: 26px;
  color: #527CCD;
}
.content{
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 22px;
  color: #527CCD;
}
.v-carousel-item{
  position: relative;
  height: 90%;
  box-shadow: 2mm;
}

</style>