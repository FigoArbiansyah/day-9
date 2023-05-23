<template>
  <nav
    class="flex justify-between items-center px-10 py-5 fixed top-0 w-full bg-white transition-all ease duration-300 z-50"
  >
    <div>
      <NuxtLink to="/" class="text-xl font-semibold">WeeQuran</NuxtLink>
    </div>
    <!-- <div>
      <input
        type="text"
        name="search"
        id="search"
        placeholder="Cari surat"
        class="outline-none border rounded px-2 py-1 focus:border-sky-500"
      />
    </div> -->
  </nav>
</template>

<script setup>
function navScroll() {
  const nav = document.querySelector("nav");
  if (document.documentElement.scrollTop > 50 || document.body.scrollTop > 50) {
    nav.classList.remove("py-5");
    nav.classList.add("py-3");
    nav.classList.add("shadow-sm");
    nav.classList.add("shadow-sky-300");
  } else {
    nav.classList.remove("py-3");
    nav.classList.add("py-5");
    nav.classList.remove("shadow-sm");
    nav.classList.remove("shadow-sky-300");
  }

  window.addEventListener("scroll", navScroll);
}

onMounted(() => {
  navScroll();
});
</script>
