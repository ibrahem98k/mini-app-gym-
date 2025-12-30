<script>
  // Baghdad, Iraq location - Al-Mansour District
  const gymLocation = {
    name: "Infinity Gym Baghdad",
    address: "Al-Mansour District, Baghdad, Iraq",
    phone: "+964 1 234 5678",
    hours: "Mon-Fri: 5:00 AM - 11:00 PM\nSat-Sun: 7:00 AM - 9:00 PM",
    mapUrl:
      "https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d13358.476421374975!2d44.34!3d33.3128!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x1557810d6b59067b%3A0x4d4c5d8f7d7a5a5a!2sAl-Mansour%2C%20Baghdad%2C%20Iraq!5e0!3m2!1sen!2s!4v1703900000000!5m2!1sen!2s",
    qrCode:
      "https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=https://maps.google.com/?q=33.3128,44.34",
  };
</script>

<div id="contact" class="card-dark animate-fade-in-up">
  <h2 class="text-2xl font-bold text-white mb-6 text-gradient">Our Location</h2>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
    <!-- Map -->
    <div class="md:col-span-2">
      <div
        class="aspect-w-16 aspect-h-9 rounded-2xl overflow-hidden bg-gray-800 shadow-inner"
      >
        <iframe
          src={gymLocation.mapUrl}
          width="100%"
          height="100%"
          style="border:0;"
          allowfullscreen=""
          loading="lazy"
          class="min-h-[300px]"
          title="Gym Location Map"
        ></iframe>
      </div>
    </div>

    <!-- Location Info -->
    <div class="space-y-5">
      <div>
        <h3 class="text-lg font-semibold text-white mb-2">Address</h3>
        <p class="text-gray-300 text-base">{gymLocation.address}</p>
      </div>

      <div>
        <h3 class="text-lg font-semibold text-white mb-2">Phone</h3>
        <a
          href={`tel:${gymLocation.phone.replace(/[^0-9+]/g, "")}`}
          class="text-red-500 hover:text-red-400 transition-colors text-base"
        >
          {gymLocation.phone}
        </a>
      </div>

      <div>
        <h3 class="text-lg font-semibold text-white mb-2">Hours</h3>
        <p class="text-gray-300 text-base whitespace-pre-line">
          {gymLocation.hours}
        </p>
      </div>

      <div class="pt-5 border-t border-gray-800">
        <p class="text-gray-400 mb-3 text-base">Scan to get directions</p>
        <div class="flex items-center space-x-4">
          <img
            src={gymLocation.qrCode}
            alt="QR Code for directions"
            class="w-24 h-24 p-2 border border-gray-700 rounded-2xl bg-white shadow-lg"
          />
          <div class="text-gray-300">
            <p class="text-sm leading-relaxed">
              Point your phone's camera at the QR code to get directions to our
              gym.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
