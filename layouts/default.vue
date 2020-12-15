<template>
  <div class="main-wrapper">
    <nav class="navbar-wrapper">
      <img class="navbar button icon" alt="Логотип" src="/logo.png" />
      <ul class="navbar ulist">
        <li class="navbar button wrapper">
          <NuxtLink to="/" class="navbar button link"
            ><img
              class="navbar button icon"
              alt="Опросы"
              src="/copy.png"
            />Опросы</NuxtLink
          >
        </li>
        <li class="navbar button wrapper">
          <NuxtLink to="/users" class="navbar button link"
            ><img
              class="navbar button icon"
              alt="Пользователи"
              src="/avatar.png"
            />Пользователи</NuxtLink
          >
        </li>
        <li class="navbar button wrapper">
          <NuxtLink to="/blacklist" class="navbar button link"
            ><img
              class="navbar button icon"
              alt="Черные списки"
              src="/speech-bubble.png"
            />Черные списки</NuxtLink
          >
        </li>
        <li class="navbar button wrapper">
          <NuxtLink to="/contacts" class="navbar button link"
            ><img
              class="navbar button icon"
              alt="Колл-центр"
              src="/telephone.png"
            />Колл-центр</NuxtLink
          >
        </li>
      </ul>

      <div class="navbar social_media">
        <NuxtLink to="/about"
          ><img
            class="navbar button icon"
            alt="Дополнительная информация"
            src="/cancel.png"
        /></NuxtLink>
      </div>
    </nav>
    <main>
      <div class="top-menu">
        <form class="searchbar wrap">
          <input
            class="searchbar inpt"
            type="text"
            placeholder="Поиск по системе"
          /><button class="searchbar btn">
            <img
              alt="Кнопка поиска"
              class="searchbar magnifying-glass"
              src="/magnifying-glass.png"
            />
          </button>
        </form>
        <div class="profileinfo-wrap">
          <img
            alt="Картинка профиля"
            class="profileinfo-avatar"
            src="https://i.redd.it/6onq25y0sh311.jpg"
          />
          <div class="profileinfo-user-info">
            <span class="profileinfo-username">Alexander C.</span>
            <span class="profileinfo-position">Администратор</span>
          </div>
        </div>
      </div>
      <Nuxt class="nuxt-component" />
    </main>
  </div>
</template>

<style >
</style>
