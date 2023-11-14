<template>
  <div>
    <div class="bg-gray-900 min-h-screen">
      <Title>{{ title }}</Title>
      <nav class="bg-gray-700 text-white shadow text-lg px-6 py-6">
        <div class="container mx-auto flex items-center justify-between px-6">
          <div>
            <NuxtLink to="/">Logo</NuxtLink>
          </div>

          <div>
            <ul class="flex space-x-12">
              <li>
                <NuxtLink to="/">Home</NuxtLink>
              </li>
              <li>
                <NuxtLink to="/personal">Personal</NuxtLink>
              </li>
              <li>
                <NuxtLink to="/house">House</NuxtLink>
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <slot />
    </div>
    <nav class="bg-gray-700 text-white shadow text-lg px-6 py-6">
      <div class="container mx-auto flex items-center justify-between px-6">
        This is the footer
      </div>
    </nav>
  </div>
</template>

<script setup>
const title = useState("title", () => "Nuxt 3 Blog");
</script>

<style>
.router-link-active {
  font-weight: bold;
  color: teal-300;
}
</style>
