<template>
  <div class="storybook-button">
    language: {{ useI18n().locale }}
  </div>
  <br>
  <button type="button" :class="classes" @click="onClick" :style="style">
    {{ t('button.label') }}
  </button>
  <div>
   <h1> {{ t('hello') }} </h1>
   <h2> {{ t('thank_you') }}</h2>
  </div>
</template>

<script lang="ts" setup>
import { useI18n } from 'vue-i18n';
import './button.css';
import { computed } from 'vue';

const props = withDefaults(defineProps<{
  /**
   * The label of the button
   */
  label: string,
  /**
   * primary or secondary button
   */
  primary?: boolean,
  /**
   * size of the button
   */
  size?: 'small' | 'medium' | 'large',
  /**
   * background color of the button
   */
  backgroundColor?: string,
}>(), { primary: false });

const emit = defineEmits<{
  (e: 'click', id: number): void;
}>();

const classes = computed(() => ({
  'storybook-button': true,
  'storybook-button--primary': props.primary,
  'storybook-button--secondary': !props.primary,
  [`storybook-button--${props.size || 'medium'}`]: true,
}));

const style = computed(() => ({
  backgroundColor: props.backgroundColor
}));

const onClick = () => {
  emit("click", 1)
};

const { t } = useI18n() // 
</script>