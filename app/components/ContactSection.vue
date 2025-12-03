<template>
  <section id="contact" class="py-16 md:py-24 bg-slate-50 dark:bg-slate-900">
    <div class="container mx-auto px-4 sm:px-6"> <!--MODIFY: Responsive padding -->
      <div class="max-w-6xl mx-auto">
        <!--Section Header -->
        <div class="text-center mb-12 md:mb-16"> <!--MODIFY: Responsive margin -->
          <!--MODIFY: Responsive font sizes -->
          <h2 class="text-4xl sm:text-5xl md:text-6xl font-bold mb-4 md:mb-6 text-slate-900 dark:text-white">
            Let's <span class="gradient-text">Connect</span>
          </h2>
          <!--MODIFY: Responsive text size and padding -->
          <p class="text-lg sm:text-xl text-slate-600 dark:text-slate-400 max-w-2xl mx-auto leading-relaxed px-4 sm:px-0">
            Ready to bring your ideas to life? Let's discuss your next project and create something amazing together.
          </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 md:gap-12 items-start"> <!--MODIFY: Responsive gap -->
          <!--Contact Information -->
          <div class="space-y-6 md:space-y-8"> <!--MODIFY: Responsive spacing -->
            <!--Introduction -->
            <div class="space-y-3 md:space-y-4"> <!--MODIFY: Responsive spacing -->
              <!--MODIFY: Responsive text sizes -->
              <h3 class="text-xl sm:text-2xl font-bold text-slate-900 dark:text-white">
                Get In Touch
              </h3>
              <p class="text-slate-600 dark:text-slate-400 text-base sm:text-lg leading-relaxed">
                I'm currently available for freelance work and full-time opportunities. 
                Whether you have a project in mind or just want to say hello, I'd love to hear from you.
              </p>
            </div>

            <!--Contact Methods -->
            <div class="space-y-3 md:space-y-4"> <!--MODIFY: Responsive spacing -->
              <div 
                v-for="contact in contactMethods"
                :key="contact.type"
                class="flex items-center space-x-3 md:space-x-4 p-4 md:p-6 bg-white dark:bg-slate-800 rounded-xl md:rounded-2xl border border-slate-200 dark:border-slate-700 hover:border-blue-500/50 transition-all duration-300 group cursor-pointer hover:shadow-lg"
                @click="handleContactClick(contact)"
              >
                <!--MODIFY: Responsive icon container -->
                <div class="w-10 h-10 md:w-14 md:h-14 bg-gradient-to-br from-blue-500 to-purple-600 rounded-lg md:rounded-xl flex items-center justify-center group-hover:scale-110 transition-transform duration-300 flex-shrink-0">
                  <span class="text-white text-base md:text-xl">{{ contact.icon }}</span>
                </div>
                <div class="flex-1 min-w-0"> <!--MODIFY: Prevent text overflow -->
                  <!--MODIFY: Responsive text sizes -->
                  <h3 class="font-semibold text-slate-900 dark:text-white text-base md:text-lg truncate">
                    {{ contact.type }}
                  </h3>
                  <p class="text-slate-600 dark:text-slate-400 text-sm md:text-base truncate">
                    {{ contact.value }}
                  </p>
                </div>
                <!--MODIFY: Responsive arrow icon -->
                <div class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 transform group-hover:translate-x-1 flex-shrink-0">
                  <svg class="w-4 h-4 md:w-5 md:h-5 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
                  </svg>
                </div>
              </div>
            

            <!--Social Links -->
            <div class="pt-4 md:pt-6"> <!--MODIFY: Responsive padding -->
              <!--MODIFY: Responsive text size -->
              <h4 class="text-base md:text-lg font-semibold text-slate-900 dark:text-white mb-3 md:mb-4">Follow my work</h4>
              <div class="flex space-x-3 md:space-x-4">
                <a 
                  v-for="social in socialLinks"
                  :key="social.name"
                  :href="social.url"
                  class="w-10 h-10 md:w-12 md:h-12 bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-lg md:rounded-xl flex items-center justify-center text-slate-600 dark:text-slate-400 hover:text-white hover:bg-blue-500 transition-all duration-300 transform hover:scale-110 group"
                  :title="social.name"
                >
                  <!--MODIFY: Responsive icon size -->
                  <span class="text-lg md:text-xl">{{ social.icon }}</span>
                </a>
              </div>
            </div>
          </div>
          </div>

          <!--Contact Form -->
          <!--MODIFY: Responsive padding and rounding -->
          <!--<div class="bg-white dark:bg-slate-800 rounded-2xl md:rounded-3xl p-6 md:p-8 border border-slate-200 dark:border-slate-700 shadow-sm hover:shadow-xl transition-all duration-300">
            MODIFY: Responsive text sizes 
            <h3 class="text-xl md:text-2xl font-bold text-slate-900 dark:text-white mb-2">Send a Message</h3>
            <p class="text-slate-600 dark:text-slate-400 text-sm md:text-base mb-6 md:mb-8">Let's start a conversation about your project</p>
            
            <form @submit.prevent="handleSubmit" class="space-y-4 md:space-y-6"> 
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6"> >
                <div class="space-y-2">
                  <label class="text-slate-700 dark:text-slate-300 text-xs md:text-sm font-semibold">Full Name *</label>
                  <input 
                    v-model="form.name"
                    type="text"
                    placeholder="Your name"
                    required
                    class="w-full px-3 py-2 md:px-4 md:py-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-lg md:rounded-xl text-slate-900 dark:text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-all duration-300 text-sm md:text-base"
                  >
                </div>

                <div class="space-y-2">
                  <label class="text-slate-700 dark:text-slate-300 text-xs md:text-sm font-semibold">Email Address *</label>
                  <input 
                    v-model="form.email"
                    type="email"
                    placeholder="your.email@example.com"
                    required
                    class="w-full px-3 py-2 md:px-4 md:py-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-lg md:rounded-xl text-slate-900 dark:text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-all duration-300 text-sm md:text-base"
                  >
                </div>
              </div>

              <div class="space-y-2">
                <label class="text-slate-700 dark:text-slate-300 text-xs md:text-sm font-semibold">Subject *</label>
                <input 
                  v-model="form.subject"
                  type="text"
                  placeholder="Project discussion"
                  required
                  class="w-full px-3 py-2 md:px-4 md:py-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-lg md:rounded-xl text-slate-900 dark:text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-all duration-300 text-sm md:text-base"
                >
              </div>

              <div class="space-y-2">
                <label class="text-slate-700 dark:text-slate-300 text-xs md:text-sm font-semibold">Message *</label>
                <textarea 
                  v-model="form.message"
                  placeholder="Tell me about your project, goals, and timeline..."
                  rows="4"
                  required
                  class="w-full px-3 py-2 md:px-4 md:py-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-lg md:rounded-xl text-slate-900 dark:text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 transition-all duration-300 resize-none text-sm md:text-base"
                ></textarea>
              </div>

              <button 
                type="submit"
                :disabled="form.loading"
                class="w-full bg-slate-900 dark:bg-white text-white dark:text-slate-900 py-3 md:py-4 rounded-lg md:rounded-xl font-semibold transition-all duration-300 hover:scale-105 hover:shadow-lg disabled:opacity-50 disabled:cursor-not-allowed disabled:transform-none flex items-center justify-center space-x-2 md:space-x-3 group text-sm md:text-base"
              >
                <span v-if="form.loading" class="animate-spin">⏳</span>
                <svg v-else class="w-4 h-4 md:w-5 md:h-5 transform group-hover:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"></path>
                </svg>
                <span>{{ form.loading ? 'Sending...' : 'Send Message' }}</span>
              </button>

              
              <div 
                v-if="form.success"
                class="p-3 md:p-4 bg-green-500/10 border border-green-500/20 rounded-lg md:rounded-xl text-green-600 dark:text-green-400 text-center animate-fade-in text-sm md:text-base"
              >
                <div class="flex items-center justify-center space-x-2">
                  <svg class="w-4 h-4 md:w-5 md:h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                  </svg>
                  <span>Message sent! I'll get back to you within 24 hours.</span>
                </div>
              </div>

              
              <div 
                v-if="form.error"
                class="p-3 md:p-4 bg-red-500/10 border border-red-500/20 rounded-lg md:rounded-xl text-red-600 dark:text-red-400 text-center animate-fade-in text-sm md:text-base"
              >
                <div class="flex items-center justify-center space-x-2">
                  <svg class="w-4 h-4 md:w-5 md:h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                  </svg>
                  <span>{{ form.error }}</span>
                </div>
              </div>
            </form>
          </div> -->
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: '',
  loading: false,
  success: false,
  error: ''
})

const contactMethods = [
  {
    type: 'Email',
    value: 'ismalizajaafar@gmail.com',
    icon: '📧',
    action: 'email'
  },
  {
    type: 'Location',
    value: 'Kuala Lumpur, Malaysia',
    icon: '📍',
    action: 'location'
  }
]

const socialLinks = [
  { name: 'GitHub', icon: '🐙', url: 'https://github.com/ismaliza' },
  { name: 'LinkedIn', icon: '💼', url: 'https://linkedin.com/in/ismaliza-jaafar' }
]

const handleContactClick = (contact) => {
  switch (contact.action) {
    case 'email':
      window.location.href = `mailto:${contact.value}`
      break
    case 'location':
      // Open Google Maps with Kuala Lumpur
      window.open('https://maps.google.com/?q=Kuala+Lumpur,Malaysia', '_blank')
      break
  }
}

const handleSubmit = async () => {
  form.loading = true
  form.error = ''
  form.success = false

  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Here you would typically send the form data to your backend
    console.log('Form submitted:', {
      name: form.name,
      email: form.email,
      subject: form.subject,
      message: form.message
    })

    // Show success message
    form.success = true
    
    // Reset form
    form.name = ''
    form.email = ''
    form.subject = ''
    form.message = ''

    // Hide success message after 5 seconds
    setTimeout(() => {
      form.success = false
    }, 5000)

  } catch (err) {
    form.error = 'Failed to send message. Please try again or email me directly at ismalizajaafar@gmail.com'
  } finally {
    form.loading = false
  }
}
</script>

<style scoped>
.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  background-size: 200% 200%;
  animation: gradient 6s ease infinite;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animate-fade-in {
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Mobile optimizations */
@media (max-width: 640px) {
  .gradient-text {
    font-size: inherit; /* Ensure gradient text scales properly */
  }
}
</style>
