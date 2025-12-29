<script>
  const features = [
    {
      title: "State-of-the-Art Equipment",
      description:
        "Our gym is equipped with the latest fitness technology and equipment from top manufacturers.",
      icon: "M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z",
    },
    {
      title: "Expert Trainers",
      description:
        "Certified personal trainers to guide you through your fitness journey with personalized plans.",
      icon: "M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z",
    },
    {
      title: "Group Classes",
      description:
        "From yoga to HIIT, we offer a variety of group fitness classes for all levels.",
      icon: "M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z",
    },
    {
      title: "24/7 Access",
      description:
        "Your fitness doesn't take a break, and neither do we. Access the gym anytime, day or night.",
      icon: "M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z",
    },
  ];

  const stats = [
    { value: "10,000+", label: "Members" },
    { value: "50+", label: "Trainers" },
    { value: "100+", label: "Classes Weekly" },
    { value: "24/7", label: "Availability" },
  ];
</script>

<section id="about" class="section-padding relative overflow-hidden">
  <div class="container-custom max-w-6xl mx-auto relative z-10">
    <!-- About Header -->
    <div
      class="text-center max-w-4xl mx-auto mb-12 md:mb-16 animate-fade-in-up"
    >
      <h2 class="text-4xl md:text-5xl font-bold text-white mb-8 text-shadow-lg">
        About Our Gym
      </h2>
      <div
        class="w-32 h-1 bg-gradient-to-r from-red-600 to-red-500 mx-auto mb-8 shadow-glow"
      ></div>
      <p class="text-xl md:text-2xl text-gray-300 leading-relaxed">
        At Infinity Gym, we're more than just a gym - we're a community of
        like-minded individuals committed to achieving their fitness goals in a
        supportive and motivating environment.
      </p>
    </div>

    <!-- Features -->
    <div
      class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-6 mb-12 md:mb-16"
    >
      {#each features as feature}
        <div
          class="bg-gradient-to-br from-gray-800 to-gray-900 p-6 rounded-2xl border border-gray-700 hover:border-red-600 transition-all duration-300 shadow-xl hover:shadow-2xl animate-fade-in-up hover:scale-105 h-full"
        >
          <div
            class="w-12 h-12 md:w-14 md:h-14 bg-red-600/20 rounded-xl flex items-center justify-center text-red-500 mb-4 hover:bg-red-600/30 transition-all duration-300"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6 md:h-8 md:w-8"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d={feature.icon}
              />
            </svg>
          </div>
          <h3 class="text-xl md:text-2xl font-semibold text-white mb-4">
            {feature.title}
          </h3>
          <p class="text-gray-300 leading-relaxed text-base md:text-lg">
            {feature.description}
          </p>
        </div>
      {/each}
    </div>

    <!-- Stats -->
    <div
      class="bg-gradient-to-r from-red-600 to-red-800 rounded-2xl p-8 md:p-10 text-white mb-12 shadow-xl shadow-glow animate-fade-in-up"
    >
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
        {#each stats as stat}
          <div>
            <div class="text-4xl md:text-5xl font-bold mb-2 text-shadow-lg">
              {stat.value}
            </div>
            <div class="text-red-100 text-lg">{stat.label}</div>
          </div>
        {/each}
      </div>
    </div>

    <!-- Testimonials -->
    <div class="mb-8 md:mb-12">
      <h3
        class="text-3xl md:text-4xl font-bold text-center text-white mb-8 md:mb-12 text-shadow-lg"
      >
        What Our Members Say
      </h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 md:gap-6">
        {#each [{ quote: "Infinity Gym has completely transformed my fitness journey. The trainers are amazing and the community is so supportive!", author: "Sarah J.", role: "Member for 2 years" }, { quote: "The 24/7 access is a game changer for my busy schedule. Best gym I've ever been to!", author: "Mike T.", role: "Member for 1 year" }, { quote: "Clean facilities, top-notch equipment, and friendly staff. Couldn't ask for more!", author: "Emma K.", role: "Member for 3 years" }] as testimonial}
          <div
            class="bg-gradient-to-br from-gray-800/90 to-gray-900/90 backdrop-blur-sm p-5 md:p-6 rounded-xl border border-gray-700/50 hover:border-red-600/50 transition-all duration-300 shadow-lg hover:shadow-xl animate-fade-in-up hover:scale-[1.02] h-full"
          >
            <div class="text-red-500 mb-4">
              {#each Array(5) as _, i}
                <span class="text-2xl">★</span>
              {/each}
            </div>
            <p class="text-gray-300 italic mb-4 text-base leading-relaxed">
              "{testimonial.quote}"
            </p>
            <div>
              <p class="font-semibold text-white text-lg">
                {testimonial.author}
              </p>
              <p class="text-gray-400 text-sm">{testimonial.role}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>
