<template>
  <div class="ui container"> 
       <div class="ui text menu">
        <div class="item">
          <NuxtLink to="/">
            <img src="~/assets/images/logo.png" alt="logo" />
          </NuxtLink>
        </div> 
        <div class="ui right item"> 
           <NuxtLink to="/"> <button @click="goBack" class="ui button green"><i class="home icon"></i> Home</button></NuxtLink>   
        </div>
      </div>

      <table class="ui celled striped table">
        <thead>
          <tr><th  >
            <h2><i class="exclamation triangle icon"></i> 404</h2>
          </th>
        </tr></thead>
        <tbody>
          <tr>
            <td class="collapsing">
               Page not found
            </td>
            
          </tr>
         
        
        </tbody>
      </table>

  </div>
</template>
