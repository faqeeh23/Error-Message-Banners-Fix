<template>
  <div class="app-container min-h-screen font-sans transition-colors duration-500 relative overflow-hidden text-gray-800 dark:text-gray-100 pb-16">
    
    <!-- Dynamic Ambient Background representing modern premium web apps -->
    <div class="absolute inset-0 z-0 overflow-hidden pointer-events-none">
      <div class="absolute w-[800px] h-[800px] rounded-full blur-[120px] top-[-200px] right-[-100px] bg-blue-400/20 dark:bg-blue-600/10 mix-blend-multiply dark:mix-blend-lighten animate-blob"></div>
      <div class="absolute w-[600px] h-[600px] rounded-full blur-[100px] bottom-[-100px] left-[-150px] bg-purple-400/20 dark:bg-purple-900/10 mix-blend-multiply dark:mix-blend-lighten animate-blob animation-delay-2000"></div>
    </div>

    <!-- Main Content wrapper for Glassmorphism -->
    <div class="relative z-10 max-w-5xl mx-auto px-6 pt-16">
      
      <!-- Sleek Header -->
      <header class="mb-14 flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
        <div>
          <h1 class="text-4xl md:text-5xl font-extrabold tracking-tight mb-3 bg-clip-text text-transparent bg-gradient-to-r from-blue-700 to-indigo-600 dark:from-blue-400 dark:to-indigo-300">
            Submitty UI Redesign
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-400 font-medium max-w-2xl">
            A standardized, accessible, and colorblind-safe implementation of system messages utilizing Okabe-Ito palettes and modern glassmorphism.
          </p>
        </div>
        <button 
          @click="toggleTheme" 
          class="group flex items-center justify-center w-12 h-12 rounded-full bg-white/50 dark:bg-gray-800/50 backdrop-blur-md border border-gray-200 dark:border-gray-700 shadow-sm hover:shadow-md hover:bg-white dark:hover:bg-gray-800 transition-all duration-300 transform hover:scale-105"
          title="Toggle Dark Mode"
        >
          <span v-if="isDark" class="text-xl">☀️</span>
          <span v-else class="text-xl">🌙</span>
        </button>
      </header>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
        <!-- LEFT HALF: The Problem (Legacy UI) -->
        <section class="flex flex-col">
          <div class="flex items-center space-x-3 mb-6">
            <div class="w-10 h-10 rounded-full bg-red-100 dark:bg-red-900/30 flex items-center justify-center text-red-600 dark:text-red-400 border border-red-200 dark:border-red-800">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
            </div>
            <h2 class="text-2xl font-bold">Legacy Interface</h2>
          </div>
          
          <div class="bg-gray-100 dark:bg-gray-800/50 rounded-2xl p-6 border border-gray-200/60 dark:border-gray-700 h-full flex flex-col space-y-6 shadow-inner">
            <p class="text-sm font-medium text-gray-500 mb-2 uppercase tracking-wide">Reliance on pure color, poor contrast</p>
            
            <div class="p-4 bg-red-600 text-white font-bold border border-black shadow-none transition-none" style="font-family: Arial;">
              Your active version was submitted 19771 days after the deadline but you have no remaining late days.<br>
              Your grade for this assignment will be recorded as a zero.<br><br>
              Contact your instructor if you believe that this is an error or that you should be granted a deadline extension.
            </div>

            <div class="p-5 bg-blue-600 text-white shadow-none transition-none" style="font-family: Arial;">
              Welcome to the Office Hours Queue page!
            </div>

            <div class="p-3 bg-yellow-200 text-black border border-gray-400 text-center shadow-none transition-none" style="font-family: Arial;">
              No late days are currently entered
            </div>

            <div class="p-6 bg-yellow-300 text-black shadow-none transition-none" style="font-family: Arial;">
              Warning: TA Beta Testing starts after submission open date. TAs will not be able to test the assignment before it is released to students.
            </div>
          </div>
        </section>

        <!-- RIGHT HALF: The Solution (Proposed UI) -->
        <section class="flex flex-col">
          <div class="flex items-center space-x-3 mb-6">
            <div class="w-10 h-10 rounded-full bg-green-100 dark:bg-green-900/30 flex items-center justify-center text-green-600 dark:text-green-400 border border-green-200 dark:border-green-800 transform hover:rotate-12 transition-transform">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>
            </div>
            <h2 class="text-2xl font-bold">Proposed Standard</h2>
          </div>
          
          <div class="bg-white/60 dark:bg-gray-900/60 backdrop-blur-xl rounded-2xl p-6 border border-white/40 dark:border-gray-700 shadow-xl shadow-blue-900/5 h-full flex flex-col relative z-20">
            <p class="text-sm font-medium text-green-600 dark:text-green-400 mb-4 uppercase tracking-wide flex justify-between items-center">
              <span>Colorblind-safe & Componentized</span>
              <button @click="resetAlerts" class="text-xs text-blue-600 hover:text-blue-800 dark:hover:text-blue-300 underline underline-offset-2">Reset</button>
            </p>
            
            <div class="flex flex-col">
              <transition-group name="list" tag="div" class="space-y-1">
                <SubmittyAlert 
                  v-if="alerts.error" 
                  key="error"
                  type="error" 
                  @close="alerts.error = false"
                >
                  <p class="font-bold mb-1">Your active version was submitted 19771 days after the deadline.</p>
                  <p class="opacity-90 leading-tight">Your grade for this assignment will be recorded as a zero. Contact your instructor if you believe that this is an error or that you should be granted a deadline extension.</p>
                </SubmittyAlert>

                <SubmittyAlert 
                  v-if="alerts.info" 
                  key="info"
                  type="info" 
                  @close="alerts.info = false"
                >
                  Welcome to the Office Hours Queue page!
                </SubmittyAlert>

                <SubmittyAlert 
                  v-if="alerts.warning" 
                  key="warning"
                  type="warning" 
                  @close="alerts.warning = false"
                >
                  TA Beta Testing starts after submission open date. TAs will not be able to test the assignment before it is released to students.
                </SubmittyAlert>
                
                <SubmittyAlert 
                  v-if="alerts.success" 
                  key="success"
                  type="success" 
                  @close="alerts.success = false"
                >
                  Your assignment was successfully submitted and the automated tests have completed.
                </SubmittyAlert>

                <!-- Test Case: Long Content Wrapping -->
                <SubmittyAlert 
                  v-if="alerts.longText" 
                  key="longText"
                  type="info" 
                  @close="alerts.longText = false"
                >
                  <p class="mb-1 font-semibold">Long Content Wrapping (Alignment Test)</p>
                  <p class="opacity-80">This is an extremely long message to test how the alert banner handles multiple lines of text. We want to ensure that the semantic icon remains fixed at the top-left rather than floating vertically to the center. It uses flexbox items-start to achieve this effect, giving the user a better reading experience.</p>
                </SubmittyAlert>
              </transition-group>
            </div>
            
            <!-- Empty state -->
            <div v-if="Object.values(alerts).every(val => !val)" class="py-12 flex flex-col items-center justify-center text-gray-500 dark:text-gray-400">
              <svg class="w-12 h-12 mb-3 opacity-50" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
              <p>All alerts dismissed</p>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import SubmittyAlert from './components/SubmittyAlert.vue';

const alerts = ref({
  error: true,
  info: true,
  warning: true,
  success: true,
  longText: true
});

const resetAlerts = () => {
  alerts.value = {
    error: true,
    info: true,
    warning: true,
    success: true,
    longText: true
  };
};

const isDark = ref(false);

const toggleTheme = () => {
  const html = document.documentElement;
  if (html.classList.contains('dark')) {
    html.classList.remove('dark');
    isDark.value = false;
  } else {
    html.classList.add('dark');
    isDark.value = true;
  }
};

onMounted(() => {
  if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    toggleTheme();
  }
});
</script>

<style>
/* Animations and global styling for premium feel */
.app-container {
  background-color: #f8fafc;
}

.dark .app-container {
  background-color: #0f172a;
}

@keyframes blob {
  0% { transform: translate(0px, 0px) scale(1); }
  33% { transform: translate(30px, -50px) scale(1.1); }
  66% { transform: translate(-20px, 20px) scale(0.9); }
  100% { transform: translate(0px, 0px) scale(1); }
}
.animate-blob {
  animation: blob 7s infinite;
}
.animation-delay-2000 {
  animation-delay: 2s;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
