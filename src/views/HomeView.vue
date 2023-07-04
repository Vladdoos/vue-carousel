<template>
  <form-info
      v-if="selectedPerson"
      :isShowForm="formVisible"
      @isVisibleForm="closeForm"
      :person="selectedPerson"
  />
  <div class="slider-container" :style="{'max-width': visibleSliderWidth + 'px'}">
    <div class="slider" ref="slider">
      <div class="slide"
           v-for="person in persons"
           :key="person.id"
           @click="showInfo(person, getPictureUrl(person.picId))">
        <img :src="getPictureUrl(person.picId)" alt="Person Image" >
        <p>{{person.name }} <br> {{person.surname}}</p>
      </div>
    </div>
    <button class="prev-button"
            v-if="currentPosition !== 0"
            @click="scroll(-1)">
      <img src="../assets/arrow.svg"></button>
    <button class="next-button"
            v-if="maxPosition !== currentPosition"
            @click="scroll(1)">
      <img src="../assets/arrow.svg"></button>
  </div>
</template>

<script>
import FormInfo from "@/components/formInfo.vue";

export default {
  name: 'HomeView',
  components: {FormInfo},
  data() {
    return {
      slideWidth: 165, // Ширина каждого блока
      visibleSlides: null, // Количество видимых блоков
      sliderWidth: null, // Ширина слайдера
      maxPosition: null, // Максимальная позиция слайдера
      currentPosition: 0, // Текущая позиция слайдера
      persons: [],
      formVisible: false,
      selectedPerson: null,
      visibleSliderWidth: null,
    };
  },
  async mounted() {
    await this.fetchPersons()
    await this.getDataSlide()
  },
  methods: {
    scroll(direction) {
      this.maxPosition = this.persons.length - this.visibleSlides
      this.currentPosition = Math.min(Math.max(this.currentPosition + direction, 0), this.maxPosition)
      this.$refs.slider.style.transform = `translateX(-${this.currentPosition * this.slideWidth}px)`
    },
    async fetchPersons() {
      await fetch('https://cdnapi.smotrim.ru/api/v1/boxes/vesti2')
          .then(response => response.json())
          .then(data => {
            // Фильтруем только "Персоны"
            this.persons = data.data.content.filter(item => item.title === 'Персоны')[0].content;
          })
          .catch(error => {
            console.error('Ошибка при получении данных:', error);
          });
    },
    // Формирование URL для картинки
    getPictureUrl (pictureId) {
      return `https://api.smotrim.ru/api/v1/pictures/${pictureId}/bq/redirect`;
    },
    // Получаем данные слайдера
    getDataSlide () {
      this.visibleSlides = Math.floor(this.$refs.slider?.offsetWidth / this.slideWidth);
      this.sliderWidth = this.slideWidth * this.persons.length;
      this.visibleSliderWidth = this.visibleSlides * 167.75
    },
    // Показываем форму
    //  Добавляем выбранного пользователя
    showInfo (person, url) {
      this.formVisible = true
      this.selectedPerson = person
      this.selectedPerson.urlImg = url
    },
    // Закрытие формы
    closeForm (data) {
      this.formVisible = data
    },
  },
  created() {
    window.addEventListener('resize', this.getDataSlide);
  },
}
</script>

<style scoped>
.slider-container {
  position: relative;
  overflow: hidden;
  max-width: 1342px;
  margin: auto;
  min-width: 168px;
}

.slider {
  display: flex;
  transition: transform 0.3s ease;
}

.slide {
  padding: 8px 8px 26px 8px;
  margin-right: 13px;
  cursor: pointer;
}
.slide:last-child{
  margin-right: 0;
}
.slide img{
  width: 138px;
  height: 138px;
  flex-shrink: 0;
  border-radius: 162px;
  cursor: zoom-in;
}
.prev-button,
.next-button {
  position: absolute;
  top: 52px;
  border-radius: 50%;
  background-color: #fff;
  font-size: 24px;
  line-height: 40px;
  text-align: center;
  cursor: pointer;
  width: 48px;
  height: 48px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 20px 0 rgba(0, 0, 0, 0.05);
  border: none;
}

.prev-button {
  left: 0;
}
.prev-button img{
  transform: rotate(180deg);
}

.next-button {
  right: 4px;
}
p{
  color: #000;
  text-align: center;
  font-size: 14px;
  font-style: normal;
  font-weight: 600;
  line-height: 16px;
  margin: 6px 0;
}
</style>
