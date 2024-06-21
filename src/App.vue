<script setup lang="ts">
import Buttons from './components/Buttons.vue'
import { ref } from 'vue'

enum BtnList {
  A = 'notSelected',
  B = 'notSelected',
  C = 'notSelected',
  D = 'notSelected',
  E = 'notSelected',
  F = 'notSelected'
}

let myBtn: BtnList = BtnList.A;

const btnListArray: string[] = Object.keys(BtnList);

const finalList = ref<string[]>([]);
function showResult(btnList: typeof BtnList) {
  for (const [key, value] of Object.entries(btnList)) {
    if (value === 'selected') {
      finalList.value.push(key);
    }
  }
  (document.getElementById('my_modal_1') as HTMLDialogElement).showModal();

}




</script>

<template>
  <div class="flex flex-row flex-wrap items-center justify-center bg-indigo-800 rounded-lg w-[70%] mx-auto mt-24 py-20"
    style="display:flex; flex-direction: row;">
    <Buttons v-for="(item, index) in btnListArray" :key="index" :text="item" :mode="BtnList[item]"
      @click="BtnList[item] == 'notSelected' ? (BtnList as any)[item] = 'selected' : BtnList[item] = 'notSelected'" />
  </div>
  <div class="flex flex-row items-center justify-center mt-12">
    <Buttons @click="showResult(BtnList)" :text="'finish'" :mode="'notSelected'" />

  </div>

  <dialog id="my_modal_1" class="modal">
    <div class="modal-box">
      <div v-if="finalList.length">
        <h1>You are Choosing Buttons of:</h1>
        <div v-for="(item, index) in finalList" :key="index" class="flex flex-row items-center justify-center mt-12">
          <p>{{ item }}</p>
        </div>
      </div>
      <div v-else>
        <p class="py-4">No one of buttons selected yet</p>
      </div>
      <div class="modal-action">
        <form method="dialog">
          <!-- if there is a button in form, it will close the modal -->
          <button class="btn">Close</button>
        </form>
      </div>
    </div>
  </dialog>
</template>

<style scoped></style>