<template>
  <div class="ui container">
    <Header />
    <div>
      <h2 class="ui left aligned header topSpace">
        Assignment 1 : List Library Shops
      </h2>

      <div>
        <p v-if="$fetchState.pending">fetching Libraries...</p>
        <p v-else-if="$fetchState.error">Error while fetching Libraries</p>

        <table class="ui single line table" v-else>
          <thead>
            <tr>
              <th>Branch Code</th>
              <th>Library Name</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="library in librariesJsonData.libraries" :key="library.alephSublibCode">
              <td>
                <NuxtLink :to="library.alephSublibCode">
                  {{ library.alephSublibCode }}
                </NuxtLink>
              </td>
              <td>{{ library.libraryName }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async fetch () {
    this.librariesJsonData = await fetch('http://infobib.bibnet.lu/bibnet-libraries.json').then(
        (res) => res.json()
    )
  },
  data () {
    return {
      librariesJsonData: []
    }
  }
}
</script>

<style>
.topSpace {
  margin-top: 20px !important;
}
</style>
