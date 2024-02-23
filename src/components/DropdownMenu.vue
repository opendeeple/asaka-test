<template>
  <div class="menu" v-bind:class="active ? 'active': ''">
    <button class="menu-button" v-on:click="active = !active">
      <img src="@/assets/icons/chevron-up.svg" v-if="active">
      <img src="@/assets/icons/chevron-down.svg" v-else>
    </button>
    <Transition>
      <div class="menu-content" v-if="active">
        <button><img src="@/assets/icons/edit.svg" /> <p>Редактировать</p></button>
        <button><img src="@/assets/icons/trash.svg" /> <p>Удалить</p></button>
      </div>
    </Transition>
  </div>
</template>

<script>
export default {
  props: {
    active: {
      type: Boolean,
      default: false,
      reactive: false
    }
  }
}
</script>