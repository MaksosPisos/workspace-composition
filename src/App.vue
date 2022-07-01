<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import ContainerList from "./components/ContainerList.vue";
import ContainerWorkspace from "./components/ContainerWorkspace.vue";
import ModalDel from "./components/ModalDel.vue";
import ModalContent from "./components/ModalContent.vue";
// реактивные элементы
const state = reactive({
  // контейнер
  containerItems: [
    {
      title: "Контейнер 1",
      active: true,
      // width: "200px",
      // heigth: "200px",
    },
  ],
  modalDel: false,
  modalContent: false,
  indexItem: undefined,
});

function addNewContainer() {
  state.containerItems.push({
    title: `контейнер ${state.containerItems.length + 1}`,
    active: false,
    // width: "200px",
    // heigth: "200px",
  });
  // console.log(state.containerItems);
}

// по клику на список контейнеров или сам контейнер делаем его активным
function changeActiveItem(index) {
  state.containerItems[index].active = true;
  state.containerItems.forEach((item, i) => {
    if (i != index) {
      item.active = false;
    }
  });
}

// модальное окно для подтверждения удаления
function delModalWindow(index) {
  state.modalDel = true;
  // state.todoItems.splice(index, 1);
  state.indexItem = index;
  // let index = state.todoItems.findIndex('')
  // console.log(index)
}
// модальное окно с контентом
function modalCont(index) {
  state.modalContent = true;
  console.log(index);
}
// удаляем контейнер из массива
function delContainerItem() {
  state.containerItems.splice(state.indexItem, 1);
  state.indexItem = undefined;
  // console.log(state.indexItem);
  closeModal();
}
// удаляем активный контейнер кнопкой в шапке
function delActiveItem() {
  state.containerItems.forEach((item, index) => {
    if (item.active === true) {
      state.modalDel = true;
      state.indexItem = index;
      // console.log(state.indexItem);
    }
  });
}
function closeModal() {
  state.modalDel = false;
  state.modalContent = false;
}
</script>

<template>
  <div data-theme="light" class="min-h-screen bg-primary-content text-neutral">
    <div class="w-[1200px] mx-auto pt-4">
      <Header
        @add-container="() => addNewContainer()"
        @del-active-container="() => delActiveItem()"
      />

      <div class="flex mt-4">
        <ul class="flex flex-col">
          <ContainerList
            v-for="(containerItem, index) in state.containerItems"
            :itemTitle="containerItem.title"
            :isActive="containerItem.active"
            @change-active="changeActiveItem(index)"
          />
        </ul>
        <ul class="flex flex-row flex-wrap gap-2 mb-10">
          <ContainerWorkspace
            v-for="(containerItem, index) in state.containerItems"
            :itemSize="[containerItem.width, containerItem.heigth]"
            :itemTitle="containerItem.title"
            @modal-window="delModalWindow(index)"
            @modal-content-window="modalCont(index)"
            :isActive="containerItem.active"
            @change-active="changeActiveItem(index)"
          />
        </ul>
      </div>
    </div>
    <ModalDel
      :switchModal="state.modalDel"
      @del-container-item="delContainerItem"
      @close-modal="closeModal"
    />
    <ModalContent :switchModal="state.modalContent" @close-modal="closeModal" />
  </div>
</template>
