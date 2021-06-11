<template>
  <div class="ui container">
    
  <div class="ui text menu">
    <div class="item">
      <NuxtLink to="/">
        <img src="~/assets/images/logo.png" alt="logo" />
      </NuxtLink>
    </div>

     
  </div>
 
    <div>
      <h2 class="ui left aligned header topSpace">
        Assignment 1 : List Library Shops
      </h2>

      <div>
        <p v-if="$fetchState.pending">fetching Libraries...</p>
        <p v-else-if="$fetchState.error">Error while fetching Libraries</p>

        <table class="ui striped line table" v-else>
          <thead>
            <tr>
              <th>Branch Code</th>
              <th>Library Name</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="library in librariesJsonData.libraries" :key="library.alephSublibCode">
              <td  >
                <h5 class="ui    aligned header"><NuxtLink :to="library.alephSublibCode" class="ui green">
                  {{ library.alephSublibCode }}
                </NuxtLink>
                </h5>
              </td>
              <td>
              <h5 class="ui    aligned header">
                <NuxtLink :to="library.alephSublibCode" class="ui green">
                   {{ library.libraryName }}
                </NuxtLink>
                </h5>
              </td>
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
    this.librariesJsonData = await fetch('http://infobib.bibnet.lu/bibnet-libraries.json' ).then(
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
