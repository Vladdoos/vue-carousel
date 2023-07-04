<template>
  <div :class="{'modal-visible': isShowForm}" class="modal" @click.self="closeForm()">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header" @click="closeForm()">
          <img :src="person.urlImg"/>
        </div>
        <div class="modal-body">
          <h1>ведущий</h1>
          <h2>{{person.name }} <br> {{person.surname}}</h2>
          <p>{{person.title}} – российский журналист и общественный деятель, ведущий на телевидении и радио, автор документальных фильмов и книг, кандидат экономических наук. </p>
          <div class="q grad">&nbsp;</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "formInfo",
  props: {
    isShowForm: Boolean,
    person: Object
  },
  data() {
    return {
    }
  },
  methods: {
    closeForm () {
      this.$emit('isVisibleForm', false);
    }
  },
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1;
  opacity: 0;
  -webkit-transition: opacity 100ms ease-in;
  -moz-transition: opacity 100ms ease-in;
  transition: opacity 100ms ease-in;
  pointer-events: none;
}
.modal-visible {
  opacity: 1;
  pointer-events: auto;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}

.modal-content {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: #fff;
  outline: 0;
  box-shadow: 0 16px 32px 0 rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  height: 380px;
  overflow: hidden;
}
.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 201px;
  overflow: hidden;
  position: relative;
  border-radius: 8px;
  cursor: zoom-out;
}

.modal-header img{
  width: 100%;
}
.modal-header::after {
  content: url('../assets/play-button.svg');
  position: absolute;
  right: 0;
  top: 0;
  width: 100px;
  height: 72px;
}

.modal-body {
  padding: 17px 16px 0 16px;
  overflow: hidden;
}
h1,h2, p{
  margin: 0 0 4px 0;
  text-align: left;
}
h1{
  color:  #B8C2CC;
  font-size: 12px;
  font-style: normal;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 1px;
  text-transform: uppercase;
  font-family: RF Dewi Condensed, sans-serif;
}
h2{
  color: #000;
  font-size: 24px;
  font-style: normal;
  font-weight: 700;
  line-height: 28px;
}
p{
  font-size: 16px;
  font-style: normal;
  font-weight: 600;
  line-height: 24px;
  border-radius: 8px;
  overflow: hidden;
}
/*@media (min-width: 576px) {*/
  .modal-dialog {
    max-width: 286px;
    margin: 80px auto;
    border-radius: 8px;
    box-shadow: 0 16px 32px 0 rgba(0, 0, 0, 0.05);
  }
/*}*/
@media (max-width: 560px) {
}
.q {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 70px;
}
.grad {
  background-image: linear-gradient(#ffffff82, #ffffffd9, #ffffff);
}
</style>
