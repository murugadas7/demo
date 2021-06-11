<template>
  <div class="ui container">
    <template>
      <div class="ui text menu">
        <div class="item">
          <NuxtLink to="/">
            <img src="~/assets/images/logo.png" alt="logo" />
          </NuxtLink>
        </div>

        <div class="ui right item">
            
                <button @click="goBack" class="ui button green"><i class="home icon"></i> Home</button>
            
        </div>
      </div>
    </template>
    <h2 class="ui header">
      <div class="ui grid">
        <div class="sixteen wide column"></div>
        <div class="sixteen wide column">
          <i class="circular book icon"></i>
          <div class="content">
            {{ libraryData.libraryName }}

            <div class="sub header">{{ libraryData.alephSublibCode }}</div>
          </div>
        </div>
         
      </div>
    </h2>

    <div class="ui placeholder segment">
      <div class="ui two column very relaxed stackable grid">
        <div class="ui column">
          <div class="ui segment">
            <div class="ui small feed">
              <h2 class="ui header">
                <i class="address card outline icon"></i>
                <div class="content">Contact Us</div>
              </h2>
              <div class="ui divider"></div>
              <div
                class="ui"
                v-for="address in libraryData.address"
                :key="address" >
                <div class="item">{{ address }}</div>
              </div>

              <div class="ui contact">
                <div
                  class="ui item"
                  v-for="email in libraryData.contact.emails"
                  :key="email.address"
                >
                  <i class="envelope icon left"></i>
                  <a :href="`mailto:${email.address}`"> {{email.address}} </a>
                </div>
              </div>
              <div class="ui contact">
                <div
                  class="ui"
                  v-for="website in libraryData.contact.websites"
                  :key="website.address"
                >
                  <i class="globe icon"></i>
                  <a :href="website.address" target="_blank">
                    {{ website.address }}
                  </a>
                </div>
              </div>
              <div class="ui contact">
                <div
                  class="ui"
                  v-for="phone in libraryData.contact.phones"
                  :key="phone.number"
                >
                  <i class="phone flipped icon"></i>
                  <a :href="`tel:${phone.number}`"> {{ phone.number }} </a>
                </div>
              </div>

              <div class="header"></div>
            </div>
          </div>

          <div class="ui column">
            <div class="ui segment">
              <div class="ui small feed">
                <h3 class="ui header">
                  <i class="exclamation triangle icon"></i> Important Notes
                </h3>
                <div class="ui divider"></div>

                <ul class="ui list" v-if="!!libraryData.access">
                  <li
                    v-for="accessNote in libraryData.access"
                    :key="accessNote"
                    v-if="!!accessNote" >
                    {{ accessNote }}
                  </li>
                </ul>
                <p v-else>No Record Found!</p>
              </div>
            </div>
          </div>
        </div>
        <div class="top aligned column">
          <div class="ui one column grid">
            <div class="column">
              <div class="ui raised segment">
                <a class="ui red ribbon label">Library Opening Hours</a>
                <span>Customers will be required to wear a face mask</span>
                <table class="ui very basic table">
                  <tbody>
                    <tr
                      v-for="(workingHours, days) in libraryData.openingHours
                        .daysTimes"
                      :key="days"
                    >
                      <td class="days">{{ days }}</td>
                      <td>
                        <div class="ui list" v-if="workingHours.length">
                          <div
                            class="item"
                            v-for="workingHour in workingHours"
                            :key="workingHour"
                          >
                            <div class="workingHours">{{ workingHour }}</div>
                          </div>
                        </div>
                        <div class="ui light-grey circular label" v-else>
                          Closed
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="ui vertical divider hide"></div>
    </div>

    <div class="ui one column grid">
      <div class="column">
        <div class="ui segment">
          <div class="ui small feed">
            <h4 class="ui header">Remarks</h4>
            <div class="ui divider"></div>
            <ul class="ui list" v-if="!!libraryData.generalRemarks">
              <li  v-for="generalRemark in libraryData.generalRemarks" :key="generalRemark"
                v-if="!!generalRemark" >
                {{ generalRemark }}
              </li>
            </ul>
            <p v-else>No Record Found!</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  transition: 'bounce',
  head () {
    return {
      title: this.libraryData.libraryName,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.libraryData.libraryName
        }
      ]
    }
  },
  async asyncData ({ params }) {
    const libraryData = await fetch(
      `http://infobib.bibnet.lu/show.php?lib=${params.alephSublibCode}&format=json&lang=eng`).then((res) => {
      if (res.ok) {
        return res.json()
      }
      throw new Error(res.status)
    })
    return { libraryData }
  },
  methods: {
    goBack () {
      return this.$router.go(-1)
    }
  }
}
</script>
<style>
.ui.vertical.divider::after,
.ui.vertical.divider::before {
  height: calc(100% - 0rem);
}

.topSpace {
  margin-top: 20px !important;
}

.workingHours {
  font-weight: 700;
  color: #21ba45;
  letter-spacing: 2px;
  font-size: 0.97em;
}

.days {
  text-transform: capitalize;
  letter-spacing: 1px;
}

.contact {
  font-size: 1.2em;
  line-height: 25px;
  color: #ff8a9b;
}

.contact a {
  color: #009e97;
  font-size: 0.9em;
  font-weight: 700;
  letter-spacing: 1px;
}

@media only screen and (max-width: 767px) {
  .hide {
    display: none;
  }

  .homeStyle {
    display: none;
  }
}
</style>
