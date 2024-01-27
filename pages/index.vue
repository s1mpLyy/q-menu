<template>
  <div
    v-if="!pending"
    id="IndexPageLayout"
    class="grid grid-cols-1 gap-4 bg-gray-100 min-h-screen"
  >
    <div class="fixed inset-0 top-3 z-0 px-4">
      <div class="inline-flex items-center gap-4">
        <div
          class="bg-gray-300 animate-pulse rounded-full mx-auto transition-all duration-200 ease-in-out flex items-center justify-center"
          :class="yScroll > 60 ? 'w-14 h-14 text-xs' : 'w-20 h-20 text-sm'"
        >
          Logo
        </div>
        <h1
          class="text-center font-semibold transition-all duration-200 ease-in-out"
          :class="yScroll > 40 ? 'text-base' : 'text-xl'"
        >
          {{ menuData.restaurant }} - {{ menuData.name }}
        </h1>
      </div>
      <img
        src="/test.png"
        class="max-h-36 object-cover object-center rounded-lg w-full mt-2"
        alt=""
      />
      <!-- <div
        class="w-full h-28 bg-gray-300 rounded-lg mt-2 bg-cover bg-center"
        style="background-image: url('/test.png')"
      ></div> -->
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
        <div
          class="flex items-center justify-between px-4 py-2 transition-all ease-linear duration-300"
          :class="yScroll > 200 ? 'h-0 hidden opacity-0' : 'h-10 opacity-100'"
        >
          <p class="font-medium text-lg">Categories</p>
          <p class="underline">See all</p>
        </div>

        <div
          class="w-full inline-flex gap-3 pb-2 items-center flex-nowrap overflow-hidden overflow-x-scroll px-4"
        >
          <NuxtLink
            v-for="(category, indexOfCategory) in menuData.categories"
            :key="indexOfCategory"
            class="px-3 py-2 inline-flex items-center justify-center gap-2 min-w-min w-max max-w-max rounded-lg shadow-sm"
            :class="
              category.name === currentSelectedCategory
                ? 'bg-gray-200'
                : 'bg-white'
            "
            :to="`#${category.id}`"
            @click="goToCategory(category.name, category.id)"
          >
            <img
              v-if="category.image"
              :src="category.image"
              class="w-5 h-5 object-cover object-center"
              alt=""
            />
            <p
              class="whitespace-nowrap"
              :class="
                category.name === currentSelectedCategory
                  ? 'text-green-900'
                  : 'text-black'
              "
            >
              {{ category.name }}
            </p>
          </NuxtLink>
        </div>
      </section>
      <section id="items" class="p-4 grid grid-cols-1 gap-4">
        <div
          v-for="(itemsInCategory, indexOfItemCategory) in menuData.categories"
          :key="indexOfItemCategory"
          class="grid grid-cols-1 gap-2 relative"
        >
          <div :id="itemsInCategory.id" class="absolute inset-0 -mt-36"></div>
          <h2 class="font-medium capitalize">
            {{ itemsInCategory.name }}
          </h2>
          <div class="grid grid-cols-2 gap-2">
            <div
              v-for="(item, indexOfCategory) in itemsInCategory.food_items"
              :key="indexOfCategory"
              class="bg-white shadow rounded-2xl overflow-hidden cursor-pointer"
            >
              <div class="relative">
                <img
                  :src="item.thumbnail"
                  class="w-full bg-cover bg-center object-cover object-center max-h-44 min-h-44"
                  alt=""
                  style="
                    background-image: url('https://storage.googleapis.com/proudcity/mebanenc/uploads/2021/03/placeholder-image.png');
                  "
                />
              </div>

              <div class="flex flex-wrap justify-between p-2">
                <p class="capitalize font-medium text-sm w-full pb-1">
                  {{ item.name }}
                </p>
                <span class="font-semibold text-sm">{{
                  item.price + " IQD"
                }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- <div
          v-for="(item, indexOfCategory) in items"
          :key="indexOfCategory"
          class="grid grid-cols-1 bg-white shadow rounded-2xl overflow-hidden cursor-pointer"
        >
          <div class="relative">
            <div v-if="item.feature.title" class="absolute top-2 left-2">
              <span class="px-1 rounded-full bg-green-300 text-xs">{{
                item.feature.title
              }}</span>
            </div>
            <img
              :src="item.image"
              class="w-full object-cover object-center max-h-44 min-h-44"
              alt=""
            />
          </div>

          <div class="flex flex-wrap justify-between p-2">
            <p class="capitalize font-medium text-sm w-full">
              {{ item.title }}
            </p>
            <span class="font-semibold text-sm">{{ item.price }}</span>
          </div>
        </div> -->
      </section>
    </div>
  </div>
</template>

<script setup>
const { data, pending } = await useFetch("https://robot-iraq.com/api/menu", {
  method: "GET",
});
if (!pending.value) console.log({ data: data.value });

const menuData = computed(() => {
  if (!pending.value && data.value.menus) {
    return data.value.menus[0];
  }
  return {};
});
const currentSelectedCategory = ref("Shisha");
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
    title: "Something to eat",
    image:
      "https://w7.pngwing.com/pngs/535/859/png-transparent-italian-cuisine-pasta-organic-food-restaurant-foods-food-recipe-cooking.png",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "12,000 IQD",
    orderDuration: "20min",
    feature: { title: "", icon: "", bg_color: "" },
  },
  {
    title: "Beaf Burger",
    image:
      "https://img.freepik.com/free-psd/zigni-isolated-transparent-background_191095-32110.jpg?w=1060&t=st=1706364438~exp=1706365038~hmac=2b620c763dc2869059168a677e06d327118e840953b3e97fa0aee6b1c9645281",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "14,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Pizza",
    image:
      "https://img.freepik.com/free-photo/isolated-shot-pizza-with-ham-arugula_181624-45431.jpg?w=1060&t=st=1706364556~exp=1706365156~hmac=1fe98f43b7bc0ac2e0a3f17a1d2798df33ee00ec9b6d696ae550bbccfcd423bc",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "8,000 IQD",
    orderDuration: "20min",
    feature: { title: "", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Paparone Pizza",
    image:
      "https://png.pngtree.com/png-clipart/20190925/original/pngtree-salami-pizza-png-image_4992988.jpg",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "9,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Pizza",
    image:
      "https://img.freepik.com/free-psd/regina-style-pizza-isolated-transparent-background_191095-24815.jpg?w=740&t=st=1706365381~exp=1706365981~hmac=b8355d43fc26dbf5d500bd3afd4fe3e8e3a43070f6dcb631b0e44f59f529e1f7",
    description: "Paparone Paparone papa papa paparone",
    category: "pizza",
    id: "1234321",
    price: "10,000 IQD",
    orderDuration: "20min",
    feature: { title: "New", icon: "", bg_color: "#FFFFFF" },
  },
  {
    title: "Test",
    image:
      "https://img.freepik.com/free-psd/view-delicious-fast-food_23-2150691793.jpg?w=360&t=st=1706365297~exp=1706365897~hmac=5624f38f857de092c1fce4fcbcf5734b8aabdf75d9922466a1c68dce94453c96",
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
    title: "Burger",
    iso: "burger",
    link: "/",
    image:
      "https://w7.pngwing.com/pngs/424/789/png-transparent-hamburger-junk-food-fast-food-hamburger-french-fries-pizza-junk-food-s-food-recipe-fast-food-restaurant.png",
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
    if (yScroll.value >= 200 && yScroll.value <= 210)
      return setTimeout(() => (yScroll.value = window.scrollY), 100);
    var scrollPosition = window.scrollY;
    yScroll.value = scrollPosition;

    return scrollPosition;
  };
}
onMounted(() => {
  detectScroll();
});
function goToCategory(name, id) {
  currentSelectedCategory.value = name;
}
</script>

<style>
* {
  scroll-behavior: smooth;
}
</style>
