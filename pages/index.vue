<template>
  <div
    id="IndexPageLayout"
    class="grid grid-cols-1 gap-4 bg-gray-100 min-h-screen"
  >
    <div class="fixed inset-0 top-4 z-0 px-4">
      <div class="inline-flex items-center gap-4">
        <div
          class="bg-gray-300 w-28 h-28 animate-pulse rounded-full mx-auto transition-all duration-500 ease-in-out"
          :class="[yScroll > 60 ? 'w-14 h-14' : '']"
        ></div>
        <h1
          class="text-center text-xl font-semibold transition-all duration-500 ease-in-out"
          :class="yScroll > 40 ? 'text-base' : ''"
        >
          Resturant Name - Menu
        </h1>
      </div>

      <div class="w-full h-28 bg-gray-300 animate-pulse rounded-lg"></div>
    </div>
    <div class="flex flex-col gap-4 bg-gray-50 rounded-2xl z-10 mt-64">
      <section id="categories" class="sticky top-0 bg-gray-50 shadow-md z-10">
        <div id="search-field" class="p-2 inline-flex items-center w-full">
          <label for="search" class="absolute px-2">
            <img src="/Search.svg" class="w-4 h-4" alt="" />
          </label>
          <input
            type="text"
            name="search"
            class="w-full h-10 px-7 pointer-events-none text-light-200 placeholder:text-[#585252] rounded-xl shadow-sm bg-light-400 border border-light-400"
            placeholder="Search for your favorite food..."
            style="box-shadow: 0px 2px 6px 0px rgba(223, 223, 232, 0.5)"
          />
        </div>
        <div class="overflow-hidden">
          <Transition name="expand">
            <div
              v-show="yScroll < 200"
              class="flex items-center justify-between px-4 py-2"
            >
              <p class="font-medium text-lg">Categories</p>
              <p class="underline">See all</p>
            </div>
          </Transition>
        </div>
        <div
          class="w-full inline-flex gap-3 pb-2 items-center flex-nowrap overflow-hidden overflow-x-scroll px-4"
        >
          <div
            v-for="(category, indexOfCategory) in categories"
            :key="indexOfCategory"
            class="bg-white px-3 py-2 inline-flex items-center justify-center gap-1 min-w-[90px] max-w-max rounded-lg shadow-sm"
          >
            <img :src="category.image" class="w-4 h-4" alt="" />
            <span class="">{{ category.title }}</span>
          </div>
        </div>
      </section>
      <section id="items" class="p-4 grid grid-cols-2 gap-4">
        <div
          v-for="(item, indexOfCategory) in items"
          :key="indexOfCategory"
          class="grid grid-cols-1 bg-white shadow rounded-2xl overflow-hidden min-w-[200px] cursor-pointer"
        >
          <div class="relative">
            <div class="absolute top-2 left-2">
              <span class="px-1 rounded-full bg-green-300 text-xs">{{
                item.feature.title
              }}</span>
            </div>
            <img
              :src="item.image"
              width="200"
              height="220"
              class="object-cover object-center"
              alt=""
            />
          </div>

          <div class="flex flex-wrap justify-between p-2">
            <p class="capitalize font-medium text-sm w-full">
              {{ item.title }}
            </p>
            <span class="font-semibold text-sm">{{ item.price }}</span>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
const yScroll = ref(0);
const items = ref([
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
]);
const categories = ref([
  {
    title: "All",
    iso: "All",
    link: "/",
    image:
      "https://image.similarpng.com/very-thumbnail/2021/07/Chef-restaurant-logo-illustrations-template-on-transparent-background-PNG.png",
  },
  {
    title: "Pizza",
    iso: "pizza",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20200401/original/pngtree-pizza-vector-illustration-png-image_5333005.jpg",
  },
  {
    title: "Pasta",
    iso: "pasta",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
  {
    title: "Pizza",
    iso: "pizza",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20200401/original/pngtree-pizza-vector-illustration-png-image_5333005.jpg",
  },
  {
    title: "Pasta",
    iso: "pasta",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
  {
    title: "Pizza",
    iso: "pizza",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
  {
    title: "Pasta",
    iso: "pasta",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
  {
    title: "Pizza",
    iso: "pizza",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
  {
    title: "Pasta",
    iso: "pasta",
    link: "/",
    image:
      "https://png.pngtree.com/png-clipart/20230102/original/pngtree-spaghetti-cartoon-png-image_8856162.png",
  },
]);
function detectScroll() {
  window.onscroll = function () {
    // Get the scroll position
    var scrollPosition = window.scrollY;
    console.log(`User Scroll : ${scrollPosition},,,var-__${yScroll.value}`);
    yScroll.value = scrollPosition;
    return scrollPosition;
  };
}
onMounted(() => {
  detectScroll();
});
</script>

<style></style>
