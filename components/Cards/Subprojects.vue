<template>
  <div>
    <!-- Start of Public Collection Table -->
    <div
      v-if="!publicCollectionLoading && publicCollections.length >= 1"
      class="mt-2 bg-white rounded-b shadow"
    >
      <div class="flex-wrap justify-between items-center px-6 py-6">
        <p class="w-full text-lg md:text-xl text-gray-800 font-semibold">
          Sub Projects ({{ publicCollections.length }})
        </p>
        <div class="mt-5 w-full overflow-auto border">
          <table
            class="border-1 border-gray-300 min-w-full bg-white dark:bg-gray-800 rounded"
          >
            <thead class="border-1 border-gray-300">
              <tr
                class="w-full h-12 border-gray-300 dark:border-gray-200 border-b py-8 bg-indigo-100"
              >
                <th
                  class="pl-6 text-gray-600 font-bold pr-6 text-left text-sm tracking-normal leading-4"
                >
                  Name
                </th>
                <td class="pr-8">
                  <button
                    class="w-32 opacity-0 bg-gray-200 transition duration-150 ease-in-out focus:outline-none focus:border-gray-800 focus:shadow-outline-gray hover:bg-gray-300 rounded text-indigo-700 px-5 py-1 text-sm cursor-default"
                  >
                    View
                  </button>
                </td>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(publicCollection, name) in publicCollections"
                :key="name"
                class="border-1 h-16 border-gray-300 border-t border-b hover:border-indigo-300 hover:shadow-md transition duration-150 ease-in-out"
              >
                <td
                  class="pl-6 pr-6 hover:underline text-left whitespace-no-wrap text-sm text-gray-800 dark:text-gray-100 tracking-normal leading-4"
                >
                  {{ publicCollections[name].name }}
                </td>
                <td class="pr-8 text-right">
                  <!-- <button
                    @click="notification = 'on'"
                    class="bg-theme-red transition duration-150 ease-in-out border border-transparent focus:outline-none focus:border-gray-800 focus:shadow-outline-gray hover:bg-theme-red-hover rounded text-white px-5 py-1 text-sm"
                  >
                    Remove
                  </button>-->
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <!-- End of Public Collection Table -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      publicCollectionLoading: true,
      publicCollectionDeleted: '',
      publicCollectionName: '',
      publicCollections: '',
      loading: '',
      data: '',
      results: '',
      ResultTitle: '',
      ResultPayload: '',
      dbname: '',
      notification: '',
    }
  },
  mounted: function () {
    this.loadPublicCollections()
  },
  methods: {
    loadPublicCollections() {
      this.$axios
        .get('https://api.apiblic.com/public/60639327caeefe2026c25e7b')
        .then((response) => {
          this.publicCollections = response.data
          this.publicCollectionLoading = false
          console.log(response.data)
        })
        .catch(() => {
          console.log('error loading public collections')
        })
    },
  },
}
</script>
