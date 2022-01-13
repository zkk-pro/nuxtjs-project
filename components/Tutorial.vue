<!-- Please remove this file from your project -->
<template>
  <div
    class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0"
  >
    <link
      href="https://unpkg.com/tailwindcss@^2/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
      <table>
        <tbody>
          <tr
            class="font-semibold text-xs md:text-lg lg:text-xl"
            v-for="item in result"
            :key="item.symbol"
          >
            <td class="px-2">
              {{ new Date().toLocaleDateString() }}
              {{ new Date().toLocaleTimeString() }}
            </td>
            <td class="px-2">{{ item.symbol }}</td>
            <td class="px-2">{{ item.priceUSD }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      result: [],
    };
  },
  methods: {
    getData() {
      const tokens = [
        "0x603c7f932ed1fc6575303d8fb018fdcbb0f39a95-bsc",
        "0xAB15B79880f11cFfb58dB25eC2bc39d28c4d80d2-bsc",
      ];
      return fetch("https://api.dex.guru/v2/tokens", {
        method: "POST",
        body: JSON.stringify({
          ids: tokens,
          network: "eth,optimism,bsc,polygon,fantom,arbitrum,celo,avalanche",
        }),
      })
        .then((res) => res.json())
        .then(({ data }) => (this.result = data));
    },
  },
  created() {
    this.getData();
    setInterval(() => {
      this.getData();
    }, 5000);
  },
};
</script>
