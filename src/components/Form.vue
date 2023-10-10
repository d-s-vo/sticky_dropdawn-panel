<script setup>
import { reactive, computed } from 'vue'

const review = reactive ({
    author: '',
    text: '',
    stars: null,
    photo: null
})

const stars = [1,2,3,4,5];

const loadPhoto = (e) => {
   const file = e.target.files[0];
   review.photo = file;
}

const previwePhoto = computed(() => {
  if(review.photo) {
   return URL.createObjectURL(review.photo);
  }  
});

function showReview () {
  console.log(review);
}

</script>

<template>
<div class="conteiner-form">
 <form 
    @submit.prevent.stop=""
    style="display:flex; flex-direction:column;">
    
    <input 
      type="text"
      v-model= "review.author"
      placeholder="Введите имя"
      style="margin-bottom: 1rem; text-align: center; "
    >

    <textarea 
      rows="4"
      v-model="review.text"
      placeholder="Ваш отзыв."
    ></textarea>  

    <h3 style="font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif; margin-bottom: 3px;">Ваша оценка</h3>
    <div 
      v-for="star in stars"
      :key="star"
    >
      <input
          v-model="review.stars" 
          :id="`star${star}`"
          :true-value="star"
          :false-value="null" 
          type="checkbox">
      <label :for="`star${star}`">{{star}}</label>
    </div>

    <div class="author__photo" style="margin-top: 1rem;">
        <label style="font-size: 18px; font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif; width: 50px; margin-bottom: 10px;">Прикрепить изображение</label>
        <input 
          type="file"
          accept="image/*"
          @change="loadPhoto">
          <img :src="previwePhoto" style="width:100px;">
    </div>

    <button 
      @click="showReview"
      class="form__btn"> Отправить </button>
  </form>
</div> 
</template>

<style lang="css">
.conteiner-form {
    width: 300px;
    margin-inline: auto;
    padding: 4px;
}

.form__btn {
  margin-top: 3px;
  margin-bottom: 3px;
  background-color: #ffa94d;
}
</style>