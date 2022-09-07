<template>
  <div class="info-panel" @click="modalState.isOpen = !modalState.isOpen" :class="isActive ? 'info-panel--active' : ''">
    <span class="name" :data-name="name">
        <span class="emoji">{{ getEmoji(name) }}</span>
        <span class="text">{{ getNameText(name) }}</span>
    </span>
    <div :style="'pointer-events: ' + (modalState.isOpen ? 'all' : 'none') + ';' +
    'transform: translateY(' + (modalState.isOpen ? '0' : '150%') + ');'"
         class="info-panel__description">
      <div class="close"></div>
      <div class="title">
        <div class="emoji">{{ getEmoji(name) }}</div>
        <div class="text">{{ getNameText(name) }}</div>
      </div>
      <div class="content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script setup>

import {defineNuxtComponent} from "nuxt/app";

defineProps(["name", "isActive"])

defineNuxtComponent({
  name: "InfoPanel",
});

let modalState = reactive({
  isOpen: false
});

let getEmoji = (baseName) => baseName.split(" ").pop()
let getNameText = (baseName) => {
  let parts = baseName.split(" ")
  parts.pop()
  return parts.join(" ")
}

</script>

<style scoped lang="scss">
@import "~/assets/css/base.scss";

.info-panel {
  display: flex;
  margin-bottom: 1em;

  @media screen and (min-width: $bp-md) {
    margin-bottom: 0;
    width: fit-content;
    height: 3em;
  }

  .name {
    width: 100%;
    text-align: center;
    border: 2px solid $c-black;
    padding: .5em 1em;
    cursor: pointer;
    position: relative;
    overflow: hidden;

    &::before {
      content: attr(data-name);
      padding: 0;
      position: absolute;
      inset: 0;
      background-color: $c-black;
      display: flex;
      justify-content: center;
      align-items: center;
      color: $c-white;
      transition: transform 150ms ease-in-out;
      transform: translateY(100%);
      transition-delay: 150ms;
    }

    &:hover {
      &::before {
        transition-delay: 0ms;
        transform: translateY(0%);
      }
    }

    @media screen and (min-width: $bp-md) {
      transition: all 250ms ease-in-out;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      width: 1em;

      &::before {
        content: unset
      }

      .text {
        overflow: hidden;
        transition: all 500ms ease-in-out;
        text-wrap: none;
        white-space: nowrap;
        transform: translateX(1em);
      }
    }
  }


  @media screen and (min-width: $bp-md) {
    &--active {
      .name {
        width: 260px;

        .text {
          display: inline-flex;
          padding-left: .5em;
          transform: translateX(0);
        }
      }
    }
  }


  &__description {
    font-size: clamp(8px, 2.6vw, 16px);
    pointer-events: none;
    transition: transform 350ms ease-in-out;
    position: fixed;
    inset: 2em;
    background-color: $c-white;
    z-index: 5;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 4em;
    text-align: center;
    border: 4px solid $c-black;
    color: $c-black;
    max-width: 1200px;
    max-height: 600px;
    margin: auto;
    transform: translateY(150%);
    overflow-y: auto;

    .close {
      position: absolute;
      top: 1em;
      right: 1em;
      width: 5em;
      height: 5em;
      cursor: pointer;

      &::before, &::after {
        content: '';
        height: 4px;
        width: 6em;
        position: absolute;
        background-color: $c-black;
        top: 50%;
        left: 50%;
        transition: width 150ms ease-in-out;
      }

      &::before {
        transform: translate(-50%, -50%) rotate(45deg);
      }

      &::after {

        transform: translate(-50%, -50%) rotate(-45deg);
      }

      &:hover {
        &::before, &::after {
          width: 4.8em;
        }
      }
    }

    .title {
      font-size: 4em;
      line-height: .9em;
      margin-bottom: 2vh;
      font-weight: bold;
      text-transform: uppercase;

      .emoji {
        font-size: 2em;
        margin-bottom: 15vh;
      }
    }

    .content {
      font-size: 2em;
      line-height: 1.1em;
    }
  }
}
</style>
