<template>
  <div>
      <input type="checkbox" class="checkbox" id="chk" @click="$emit('toggle')" />
      <label class="label" for="chk">
        <div class="ball" :class="{ darkMode: darkMode }"></div>
      </label>
    </div>
</template>
