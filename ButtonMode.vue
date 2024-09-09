<script setup>
const userPrefersDark = usePreferredDark();
const tcookie = useCookie('theme');
const currentTheme = ref('');

onMounted(() => {
  if (userPrefersDark.value) {
    currentTheme.value = 'dark';
    document.documentElement.classList.add('dark');
  } else {
    currentTheme.value = 'light';
    document.documentElement.classList.remove('dark');
  }

  if (!tcookie.value) {
    tcookie.value = currentTheme.value;
  }
});

const changeTheme = () => {
  if (currentTheme.value === 'light') {
    currentTheme.value = 'dark';
    document.documentElement.classList.add('dark');
  } else {
    currentTheme.value = 'light';
    document.documentElement.classList.remove('dark');
  }
  tcookie.value = currentTheme.value;
};

watch(userPrefersDark, () => {
  changeTheme();
});
</script>

<template>
  <!-- Иконка солнца для светлой темы -->
  <div
    class="flex cursor-pointer items-center text-3xl max-xl:justify-center max-xl:mb-2"
    :class="{
      'hidden pointer-events-none': currentTheme === 'light',
      'flex pointer-events-auto': currentTheme === 'dark'
    }"
    @click="changeTheme"
  >
    <Icon name="i-typcn-adjust-brightness" style="color: white" />
  </div>

  <!-- Иконка луны для тёмной темы -->
  <div
    class="flex cursor-pointer items-center text-3xl max-xl:justify-center max-xl:mb-2"
    :class="{
      'hidden pointer-events-none': currentTheme === 'dark',
      'flex pointer-events-auto': currentTheme === 'light'
    }"
    @click="changeTheme"
  >
    <Icon name="i-typcn-weather-night" style="color: white" />
  </div>
</template>
