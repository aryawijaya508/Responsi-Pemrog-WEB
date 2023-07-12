<script setup>
import { Head, Link } from "@inertiajs/vue3";
import { onMounted, ref } from "vue";
import { LottieAnimation } from "lottie-web-vue";
import WatermelonJSON from "/public/img/robot.json";

// Menginisialisasi variabel anim sebagai referensi Vue
let anim = ref();

// Menjalankan kode setelah komponen dipasang (mounted)
onMounted(() => {
  // Menunggu 500ms sebelum menjalankan kode berikutnya
  setTimeout(() => {
    // Menggunakan metode goToAndPlay dari animasi Lottie dengan parameter 150
    // untuk memulai animasi pada frame 150, dengan loop (true)
    console.log(anim.value.goToAndPlay(150, true));
    // Memanggil objek anim.value untuk menjalankan animasi Lottie
    anim.value.play();
  }, 500);
});

// Mendefinisikan properti komponen
const props = defineProps({
  canLogin: Boolean,
  canRegister: Boolean,
  slider: Array,
  about: Array,
  skill: Array,

  laravelVersion: { type: String, required: true },
  phpVersion: { type: String, required: true },
  options: {
    theme: {
      controlsView: "standard",
      active: "light",
      light: {
        color: "#3D4852",
        backgroundColor: "#fff",
        opacity: "0.7",
      },
      dark: {
        color: "#fff",
        backgroundColor: "#202020",
        opacity: "0.7",
      },
    },
  },
});
const showingNavigationDropdown = ref(false);
</script>

<template>
  <Head title="Welcome" />
  <nav class="bg-white border-gray-200">
    <div class="max-w-screen-xl flex flex-wrap items-center justify-between lg:mx-32 p-4">
      <a href="#" class="flex items-cente font-bold pb-1 text-xl text-green-500">
        <!-- <img src="../../Components/img/sekai_logo.svg" class="h-8 mr-3" alt="Irvan" /> -->
        <h1 class="">Arya Snack</h1>
      </a>
      <button
        @click="showingNavigationDropdown = !showingNavigationDropdown"
        id="toggleNavbar"
        type="button"
        class="inline-flex items-center p-2 ml-3 text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200">
        <span class="sr-only">Open main menu</span>
        <svg class="w-6 h-6" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd"></path>
        </svg>
      </button>
      <div :class="{ block: showingNavigationDropdown, hidden: !showingNavigationDropdown }" class="sm:hidden w-full md:block md:w-auto" id="navbarDefault">
        <ul class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 md:mt-0 md:border-0 md:bg-white">
          <li>
            <a href="#" class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-blue-500 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0">Home</a>
          </li>
          <li>
            <a href="#" class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-blue-500 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0">About</a>
          </li>
          <li>
            <a href="#" class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-blue-500 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0">Services</a>
          </li>
          <li>
            <a href="#" class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-blue-500 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0">Pricing</a>
          </li>
          <li>
            <a href="#" class="block py-2 pl-3 pr-4 text-gray-900 rounded hover:bg-blue-500 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 mb-5">Contact</a>
          </li>
          <li>
            <div v-if="canLogin">
              <Link
                v-if="$page.props.auth.user"
                :href="route('dashboard')"
                class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-md text-sm px-4 py-2 text-center mr-3 md:mr-0">
                Dashboard
              </Link>
              <template v-else>
                <Link :href="route('login')" type="button" class="text-white bg-green-500 hover:bg-green-400 font-medium rounded-md text-sm px-4 py-2 text-center mr-3 md:mr-0"> Log in</Link>
                <Link :href="route('register')" type="button" class="text-green-500 ml-2 border-2 border-green-500 hover:bg-green-200 font-medium rounded-md text-sm px-4 py-2 text-center mr-3 md:mr-0">Register</Link>
              </template>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <section class="hero lg:ml-[95px]">
    <div class="container px-5 py-5">
      <div class="flex flex-col-reverse lg:flex-row items-center lg:py-5 lg:order-first">
        <div class="lg:w-6/12 lg:ms-10 text-black">
          <div v-for="item in skill" :key="item.id">
            <h1 v-if="item && item.judul" class="text-4xl font-bold leading-tight mb-3">{{ item.judul }}</h1>
            <p v-if="item && item.konten" class="text-lg">
              {{ item.konten }}
            </p>
          </div>
          <div>
            <h2 class="text-green-600 font-bold text-xl">Halo semuanya, selamat datang di </h2>
            <h1 class="font-bold text-3xl bg-gradient-to-r py-1 from-green-500 to-green-200 bg-clip-text text-transparent">Arya Snack</h1>
            <h2 class="text-lg text-green-400 pb-2"> Apapun kegiatannya, Arya Snack pilihannya!</h2>
            <p class="text-slate-500">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Laudantium hic odio officia molestias sapiente error nemo aut laboriosam qui fugiat earum, consequatur consectetur expedita praesentium tempora rerum, et aliquid. Vitae!
            </p>
          </div>
          <div class="grid grid-cols-1 gap-2 md:flex md:justify-start">
            
            <button type="button" class=" bg-green-500 hover:bg-green-400 text-white rounded-lg px-4 py-2 mt-7">
              Get Started 
            </button>
            <button type="button" class="bg-white border-2 border-green-500 hover:bg-green-200 text-green-500 rounded-lg px-4 py-2 mt-7">Default</button>
          </div>
        </div>
        <div class="lg:w-6/12">
          <div class="mx-auto lg:w-[400px] lg:h-[400px]">
            <LottieAnimation :animation-data="WatermelonJSON" :auto-play="true" :height="150" :loop="true" :speed="0.8" ref="anim" />
          </div>
        </div>
      </div>
    </div>
  </section>
  <footer>
    <div className="mx-auto max-w-screen-xl  px-4 sm:px-6">
      <div className="grid sm:grid-cols-12 gap-8 py-8 md:py-12 border-t border-gray-200">
        <div className="sm:col-span-12 lg:col-span-3">
          <div className="mb-2">
            <Logo />
          </div>
          <div className="text-sm text-gray-600">
            <!-- <img src="../../Components/img/sekai_logo.svg" class="h-8 mr-3" alt=" Logo" /> -->
            <span class="self-center flex text-2xl font-semibold whitespace-nowrap text-black uppercase pb-1">Aryawijaya</span>
            <span class="text-xl font-semibold whitespace-wrap text-bslate-600 mb-1">21.11.4298</span>
          </div>
        </div>
        <div className="sm:col-span-6 md:col-span-3 lg:col-span-2">
          <h6 className="text-gray-800 font-medium mb-2">Products</h6>
          <ul className="text-sm">
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Web Studio</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">DynamicBox Flex</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Programming Forms</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Integrations</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Command-line</a>
            </li>
          </ul>
        </div>
        <div className="sm:col-span-6 md:col-span-3 lg:col-span-2">
          <h6 className="text-gray-800 font-medium mb-2">Resources</h6>
          <ul className="text-sm">
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Documentation</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Tutorials & Guides</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Blog</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Support Center</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Partners</a>
            </li>
          </ul>
        </div>
        <div className="sm:col-span-6 md:col-span-3 lg:col-span-2">
          <h6 className="text-gray-800 font-medium mb-2">Company</h6>
          <ul className="text-sm">
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Home</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">About us</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Company values</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Pricing</a>
            </li>
            <li className="mb-2">
              <a href="#0" className="text-gray-600 hover:text-gray-900 transition duration-150 ease-in-out">Privacy Policy</a>
            </li>
          </ul>
        </div>
        <div className="sm:col-span-6 md:col-span-3 lg:col-span-3">
          <h6 className="text-gray-800 font-medium mb-2">Subscribe</h6>
          <p className="text-sm text-gray-600 mb-4">Get the latest news and articles to your inbox every month.</p>
          <form>
            <div className="flex flex-wrap mb-4">
              <div className="w-full">
                <label className="block text-sm sr-only" htmlFor="newsletter">Email</label>
                <div className="relative flex items-center max-w-xs">
                  <input id="newsletter" type="email" className="form-input w-full text-gray-800 px-3 py-2 pr-12 text-sm" placeholder="Your email" required />
                  <button type="submit" className="absolute inset-0 left-auto" aria-label="Subscribe">
                    <span className="absolute inset-0 right-auto w-px -ml-px my-2 bg-gray-300" aria-hidden="true"></span>
                    <svg className="w-3 h-3 fill-current text-blue-600 mx-3 shrink-0" viewBox="0 0 12 12" xmlns="http://www.w3.org/2000/svg">
                      <path d="M11.707 5.293L7 .586 5.586 2l3 3H0v2h8.586l-3 3L7 11.414l4.707-4.707a1 1 0 000-1.414z" fillRule="nonzero" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
      <div className="md:flex md:items-center md:justify-between py-4 md:py-8 border-t border-gray-200">
        <ul className="flex mb-4 md:order-1 md:ml-4 md:mb-0">
          <li>
            <a href="#0" className="flex justify-center items-center text-gray-600 hover:text-gray-900 bg-white hover:bg-white-100 rounded-full shadow transition duration-150 ease-in-out" aria-label="Twitter">
              <svg className="w-8 h-8 fill-current" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M24 11.5c-.6.3-1.2.4-1.9.5.7-.4 1.2-1 1.4-1.8-.6.4-1.3.6-2.1.8-.6-.6-1.5-1-2.4-1-1.7 0-3.2 1.5-3.2 3.3 0 .3 0 .5.1.7-2.7-.1-5.2-1.4-6.8-3.4-.3.5-.4 1-.4 1.7 0 1.1.6 2.1 1.5 2.7-.5 0-1-.2-1.5-.4 0 1.6 1.1 2.9 2.6 3.2-.3.1-.6.1-.9.1-.2 0-.4 0-.6-.1.4 1.3 1.6 2.3 3.1 2.3-1.1.9-2.5 1.4-4.1 1.4H8c1.5.9 3.2 1.5 5 1.5 6 0 9.3-5 9.3-9.3v-.4c.7-.5 1.3-1.1 1.7-1.8z" />
              </svg>
            </a>
          </li>
          <li className="ml-4">
            <a href="#0" className="flex justify-center items-center text-gray-600 hover:text-gray-900 bg-white hover:bg-white-100 rounded-full shadow transition duration-150 ease-in-out" aria-label="Github">
              <svg className="w-8 h-8 fill-current" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
                <path
                  d="M16 8.2c-4.4 0-8 3.6-8 8 0 3.5 2.3 6.5 5.5 7.6.4.1.5-.2.5-.4V22c-2.2.5-2.7-1-2.7-1-.4-.9-.9-1.2-.9-1.2-.7-.5.1-.5.1-.5.8.1 1.2.8 1.2.8.7 1.3 1.9.9 2.3.7.1-.5.3-.9.5-1.1-1.8-.2-3.6-.9-3.6-4 0-.9.3-1.6.8-2.1-.1-.2-.4-1 .1-2.1 0 0 .7-.2 2.2.8.6-.2 1.3-.3 2-.3s1.4.1 2 .3c1.5-1 2.2-.8 2.2-.8.4 1.1.2 1.9.1 2.1.5.6.8 1.3.8 2.1 0 3.1-1.9 3.7-3.7 3.9.3.4.6.9.6 1.6v2.2c0 .2.1.5.6.4 3.2-1.1 5.5-4.1 5.5-7.6-.1-4.4-3.7-8-8.1-8z" />
              </svg>
            </a>
          </li>
          <li className="ml-4">
            <a href="#0" className="flex justify-center items-center text-gray-600 hover:text-gray-900 bg-white hover:bg-white-100 rounded-full shadow transition duration-150 ease-in-out" aria-label="Facebook">
              <svg className="w-8 h-8 fill-current" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
                <path d="M14.023 24L14 17h-3v-3h3v-2c0-2.7 1.672-4 4.08-4 1.153 0 2.144.086 2.433.124v2.821h-1.67c-1.31 0-1.563.623-1.563 1.536V14H21l-1 3h-2.72v7h-3.257z" />
              </svg>
            </a>
          </li>
        </ul>
        <div className="text-sm text-gray-600 mr-4">Copyright &copy; 2023, Aryawijaya. All rights reserved.</div>
      </div>
    </div>
  </footer>
</template>
<style></style>