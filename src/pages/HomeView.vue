<template>
  <main>
    <section class="menu"></section>
    <section class="container">
      <div class="header">
        <i class="ri-menu-line menu-icon"></i>
        <h2>Your Organisation</h2>
        <div class="circle"></div>
      </div>
      <div class="employees-container">
        <div class="emp-cards-container">
          <div class="emp-cards-header">
            <h2>{{ sortedUsers.length }} Employees</h2>
            <div class="filter-dropdown-container">
              <button class="filter-button" @click="showDropdown = !showDropdown">
                <i class="ri-filter-line filter-icon"></i>
                <p>Filter</p>
              </button>
              <div class="filter-dropdown" :class="{ 'dropdown-active': showDropdown, 'dropdown-inactive': !showDropdown }">
                <ul>
                  <li><input v-model="statusArray" value="active" type="checkbox">Active</li>
                  <li><input v-model="statusArray" value="unactive" type="checkbox">Unactive</li>
                  <li><input v-model="statusArray" value="unverified" type="checkbox">Unverified</li>
                </ul>
                <button 
                  @click="sortUsers(), showDropdown = !showDropdown" 
                  class="filter-submit-button"> Search
                </button>
              </div>
            </div>
          </div>
          <div class="emp-cards">
            <EmployeeCard 
              v-for="user in sortedUsers" 
              :key="user.id" 
              :emp-data="user"
            />
          </div>
          <div class="emp-cards-footer">
            <h3>View</h3>
          </div>
        </div>
        <div class="right-nav">
          <div class="circle"></div>
          <div class="circle"></div>
          <div class="circle"></div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>

import EmployeeCard from "../components/EmployeeCard.vue";
import userData from "../users.json"

export default {
  name: "HomeView",
  components: {
    EmployeeCard,
  },

  data() {
    return {
      users: [],
      sortedUsers: [],
      showDropdown: false,
      statusArray: [],
      maxUsersInSinglePage: 12,
    };
  },

  mounted() {
    this.users = userData.users;
    
    // if(this.users.length > this.maxUsersInSinglePage)
    //   this.sortedUsers = this.users.slice(0, this.maxUsersInSinglePage);
    // else 
    this.sortedUsers = this.users;
    // console.log(this.users[0].status);
  },

  methods: {
    printStatus() {
      console.log(this.statusArray[0]);
    },

    sortUsers() {
      if (this.statusArray.length === 0) {
        this.sortedUsers = this.users;
        return;
      }

      this.sortedUsers = this.users.filter(data => {
        for (var i = 0; i < this.statusArray.length; i++) {
          if(data.status == this.statusArray[i])
            return true;
        }
      });
      console.log(this.sortedUsers);
    }
  }
};

</script>

<style lang="scss">

  .circle {
    height: 40px;
    width: 40px;
    border-radius: 100%;
    background-color: lightgrey;
  }

  .dropdown-active {
    display: flex;
    flex-direction: column;
    min-width: 120px;
  }

  .menu-icon, .dropdown-inactive {
    display: none;
  }

  main {
    display: flex;
    min-height: 100vh;

    .menu {
      flex-basis: 15%;
      background-color: #1c212d;
    }

    .container {
      flex-basis: 85%;
      background-color: #f2f7fa;
      display: flex;
      flex-direction: column;

      .header {
        padding: .75rem 1rem;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 1px solid lightgray;
        background-color: #ffffff;

        h2 {
          font-size: 1.3rem;
        }
      }

      .employees-container {
        display: flex;
        background-color: #eff1f3;
        height: 100%;

        .right-nav {
          display: flex;
          flex-direction: column;
          padding: 1rem;
          gap: 1rem;
          border-left: 1px solid lightgray;
          background-color: #ffffff;
        }

        .emp-cards-container {
          display: flex;
          background-color: #eff1f3;
          height: 100%;
          flex-direction: column;
          width: 100%;

          .emp-cards-header {
            display: flex;
            align-items: center;
            padding: 1.5rem 2rem;
            gap: 2rem;

            h2 {
              letter-spacing: 1.5px;
              font-size: 1.5rem;
            }

            .filter-dropdown-container {
              position: relative;

              .filter-button {
                display: flex;
                padding: .5rem 1rem;
                gap: .5rem;
                border-radius: 4px;
                background-color: #ffffff;
                color: #8b98a1;
                box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
                font-size: 1.2rem;

                .filter-icon {
                  font-size: 1.5rem;
                } 
              }

              .filter-dropdown {
                margin-top: .5rem;
                position: absolute;
                padding: 1rem;
                background-color: #fff;
                border-radius: 4px;
                box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;

                ul {
                  display: flex;
                  flex-direction: column;
                  gap: .5rem;
                }

                ul > li > input {
                  margin-right: 8px;
                }

                .filter-submit-button {
                  margin-top: 1rem;
                  margin-right: auto;
                  border-radius: 4px;
                  padding: .25rem .5rem;
                  font-size: .8rem;
                }
              }
            }
          }

          .emp-cards {
            padding: 2rem;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(14rem, 1fr));
            grid-gap: 1rem;
          }

          .emp-cards-footer {
            display: flex;
            padding: 0 2rem 1.5rem 2rem;
            color: #b9bfc6;
          }
        }
      }
    }
  }

  @media (min-width: 320px) and (max-width: 812px) {

    main {
      .menu {
        display: none;
      }

      .container {
        flex: 1;

        .employees-container {
          .emp-cards-container > .emp-cards-header {
            padding-bottom: 0;
            h2 {
              font-size: 1.2rem;
            }
            .filter-dropdown-container > .filter-button {
              font-size: .8rem;

              .filter-icon {
                font-size: 1rem;
              }
            }

            .filter-dropdown-container > .filter-dropdown {
              font-size: .8rem;
              right: 0;
            }
          }

          .right-nav {
            display: none;
          }
        }
      }
    } 

    .circle {
      height: 30px;
      width: 30px;
    }

    .menu-icon {
      display: block;
      font-size: 1.3rem;
    }

    .emp-cards-header {
      justify-content: space-between;
    }
  }

</style>