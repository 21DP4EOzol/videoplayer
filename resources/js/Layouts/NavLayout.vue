<script setup>
import { ref, onMounted } from 'vue';
import { usePage, Link } from '@inertiajs/vue3';
import MenuIcon from 'vue-material-design-icons/Menu.vue';
import MagnifyIcon from 'vue-material-design-icons/Magnify.vue';
import SideNavitem from '@/Components/SideNavitem.vue';

let openSideNav = ref(true);
let openSideNavOverlay = ref(false);
let sideNavOverlay= ref(null);
let width = ref(document.documentElement.clientWidth);

onMounted(()=>{
    resize()
    sideNavOverlay.value.classList.value = sideNavOverlay.value.classList.value += ' hidden'
    window.addEventListener('resize', ()=>{
        width.value = document.documentElement.clientWidth;
        resize()
    });
})

const resize = () => {
    if (width.value < 1280 && openSideNav.value){
        openSideNav.value = false
    }
    if (width.value > 1279 && !openSideNav.value){
        openSideNav.value = true
    }
}

const isnavOverlay = () => {
    if(usePage().url === '/') openSideNav.value = !openSideNav.value
    if(usePage().url === '/add-video') openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().url === '/delete-video') openSideNavOverlay.value = !openSideNavOverlay.value
    if(width.value , 640) openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().url !== '/' && width.value < 640) openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().props.video) openSideNavOverlay.value = !openSideNavOverlay.value
    if (usePage().url === '/') {openSideNav.value = !openSideNav.value;}
    if (usePage().url === '/add-video' || usePage().url === '/delete-video' || width.value < 640) {openSideNavOverlay.value = !openSideNavOverlay.value;}
    if (usePage().props.video) {openSideNavOverlay.value = !openSideNavOverlay.value;}
    
    
    
}

</script>

<template>
    <div class="relitive">
        <div id="TopNav" class="w-[100%] h-[60px] bg-black z-20 flex items-center justify-between">
            <div class="flex items-center">
                <button @click="isnavOverlay()" class="p-2 ml-3 rounded-full hover:bg-gray-800 inline-block cursor-pointer">
                    <MenuIcon fillColor="#FFFFFF" :size="26"/>
                </button>
                <div class="mx-2"></div>
                <Link :href="route('home')" class="flex text-white items-center justify-center mr-10 cursor-pointer">
                    <img width="32" src="/images/YT-logo.png" alt="">
                    <img width="32" src="/images/YT-logo-text.png" alt="">
                </Link>   
            </div>

            <div class="w-[600px] md:block hidden">
                <div class="rounded-full flex items-center bg-[#222222]">
                    <input type="text" class="
                    form-control
                    block
                    w-full
                    px-5 
                    py-1.5 
                    text-base 
                    font-normal 
                    text-gray-200 
                    bg-black 
                    placeholder-gray-400 
                    bg-clip-padding 
                    border 
                    border-solid 
                    border-l-gray-700 
                    border-y-gray-700 
                    rounded-l-full 
                    transition 
                    ease-in-out 
                    m-0 
                    border-transparent
                    focus:ring-0"
                    placeholder="Search"
                    />
                    <MagnifyIcon class="mx-6" fillColor="#FFFFFF" :size="23"/>
                </div>
            </div>
            <div>
                <img
                    class="rounded-full mx-8"
                    width="35"
                    src="https://yt3.ggpht.com/yti/ANjgQV_iuVcS1YF6ZFK5prAw5JsQZSbJydiHJ3-hIop3c_hj_Nc=s88-c-k-c0x00ffffff-no-rj"
                >
            </div>
        </div>

        <div v-if="width > 639">
        
            <div
            v-if="$page.url === '/'"
            id="SideNav" 
            class="h-[100%] fixed z-0 bg-black"
            :class="[!openSideNav ? 'w-[70px]' : 'w-[240px]']"
        >
            <ul :class="[!openSideNav ? 'p-2' : 'px-5 pb-2 pt-[7px]']" class ="mt-[60px] w-full">
                <Link :href="route('home')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Home"/>
                </Link>
                <Link :href="route('addVideo')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Add Video"/>
                </Link>
                <Link :href="route('deleteVideo')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Delete Video"/>
                </Link>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <SideNavitem :openSideNav="openSideNav" iconString="Subscription"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Library"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Liked"/>
                <SideNavitem :openSideNav="openSideNav" iconString="History"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5" />
                    <div class="text-gray-400 text-[14px] text-extrabold">
                    About Press Copyright
                    <div>Contact us</div>
                    Creator Advertise Developers
                </div>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <div class="text-gray-400 text-[14px] text-extrabold">
                    Terms Privacy Policy & Safety
                    <div>How Youtube works</div>
                    <span>Test new features</span>
                </div>
                </div>
            </ul>
        </div>

        </div>


        <div
            v-if="$page.url === '/'"
            id="SideNav" 
            class="h-[100%] fixed z-0 bg-black"
            :class="[!openSideNav ? 'w-[70px]' : 'w-[240px]']"
        >
            <ul :class="[!openSideNav ? 'p-2' : 'px-5 pb-2 pt-[7px]']" class ="mt-[60px] w-full">
                <Link :href="route('home')">
                    <SideNavitem :openSideNav="true" iconString="Home"/>
                </Link>
                <Link :href="route('addVideo')">
                    <SideNavitem :openSideNav="true" iconString="Add Video"/>
                </Link>
                <Link :href="route('deleteVideo')">
                    <SideNavitem :openSideNav="true" iconString="Delete Video"/>
                </Link>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <SideNavitem :openSideNav="openSideNav" iconString="Subscription"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Library"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Liked"/>
                <SideNavitem :openSideNav="openSideNav" iconString="History"/>
                <SideNavitem :openSideNav="openSideNav" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5" />
                    <div class="text-gray-400 text-[14px] text-extrabold">
                    About Press Copyright
                    <div>Contact us</div>
                    Creator Advertise Developers
                </div>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <div class="text-gray-400 text-[14px] text-extrabold">
                    Terms Privacy Policy & Safety
                    <div>How Youtube works</div>
                    <span>Test new features</span>
                </div>
                </div>
            </ul>
        </div>

        <div 
            @click="openSideNavOverlay = false"
            class="bg-black bg-opacity-70 fixed z-50 w-full h-screen" 
            :class="
                openSideNavOverlay
                ? 'animate__animated animate__fadeIn animate__faster'
                : 'hidden z-[-1]'
            "
        />

        <div>
            <div
            id="SideNavOverlay" 
            ref="sideNavOverlay"
            class="h-[100%] fixed z-50 bg-black mt-[9px] w-[240px]"
            :class="[
                openSideNavOverlay 
                ? 'animate__animated animate__slideInLeft animate__faster' 
                : 'animate__animated animate__slideOutLeft animate__faster'
            ]"
        >
            <div class="flex items-center">
                
                <div class="mx-2"></div>
                <div class="flex text-white items-center justify-center mr-10 cursor-pointer">
                    
                </div>   
            </div>
            <ul class ="w-full px-5 py-2 p-2 mt-2">
                <Link :href="route('home')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Home"/>
                </Link>
                <Link :href="route('addVideo')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Add Video"/>
                </Link>
                <Link :href="route('deleteVideo')">
                    <SideNavitem :openSideNav="openSideNav" iconString="Delete Video"/>
                </Link>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <SideNavitem :openSideNav="true" iconString="Subscription"/>
                <SideNavitem :openSideNav="true" iconString="Library"/>
                <SideNavitem :openSideNav="true" iconString="Liked"/>
                <SideNavitem :openSideNav="true" iconString="History"/>
                <SideNavitem :openSideNav="true" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5" />
                    <div class="text-gray-400 text-[14px] text-extrabold">
                    About Press Copyright
                    <div>Contact us</div>
                    Creator Advertise Developers
                </div>
                <div class="border-b border-b-gray 700 my-2.5"></div>
                <div class="text-gray-400 text-[14px] text-extrabold">
                    Terms Privacy Policy & Safety
                    <div>How Youtube works</div>
                    <span>Test new features</span>
                </div>
                </div>
            </ul>
        </div>
        </div>
        <div
            class="w-[100%] h-[calc(100vh-60px)] absolute right-0 top-[60px]"
            :class="{
                'w-[calc(100%-70px)]': !openSideNav,
                'w-[calc(100%-240px)]': openSideNav,
                'w-[100w] xl:w-[calc(100%-80px)]': $page.url !== '/',
                'w-[100vw]': width < 639
            }"
        >

            <slot/>
        </div>
    </div>
</template>

<style>
    body {
        background-color: black;
    }
</style>
