<template>
  <div class="emp-card">
    <div class="emp-card-header">
      <div class="status" :class="classBasedOnStatus(empData.status)"> {{ empData.status }} </div>
      <div class="option-button">
        <i v-for="i in 3" :key="i" class="ri-checkbox-blank-circle-fill" style="font-size: 4px"></i>
      </div>
    </div>
    <img src="../assets/avatar-male.jpg" alt="Profile Photo">
    <h1>{{ empData.name }}</h1>
    <h2>{{ empData.designation }}</h2>
    <div class="emp-card-body">
      <div class="details">
        <h3>Department</h3>
        <h2> {{ empData.department }}</h2>
      </div>
      <div class="details">
        <h3>Date Hired</h3>
        <h2> {{ empData.dateHired }}</h2>
      </div>
      <div class="contact">
        <div class="row">
          <i class="ri-mail-line"></i>
          <h2>{{ empData.email }}</h2>
        </div>
         <div class="row">
          <i class="ri-phone-line"></i>
          <h2>+{{ empData.phone }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "EmployeeCard",
  props: ['empData'],

  methods: {
    classBasedOnStatus(status) {
      if (status === "active") {
        return "active";
      } else if (status === "unactive") {
        return "unactive";
      } else {
        return "unverified";
      }
    }
  }
};

</script>

<style lang="scss">

  @keyframes fade-in {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  .status {
    font-size: .6rem;
    font-weight: 500;
    border-radius: 4px;
    text-transform: capitalize;
    padding: .25rem .5rem;
    margin-left: auto;
    margin-right: .5rem;
  }

  .active {
    background-color: #edfcf5;
    color: #4d977c;
    border: .5px solid #4d977c;
  }

  .unactive {
    background-color: #ffeaea;
    color: #d55557;
    border: .5px solid #d55557;
  }

  .unverified {
    background-color: #fff4e6;
    color: #ffd831;
    border: .5px solid #ffd831;
  }

  .emp-card {
    display: flex;
    flex-direction: column;
    background-color: #ffffff;
    border-radius: 8px;
    padding: .5rem;
    gap: .5rem;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
    // transition: all ease-in 300ms;
    animation: fade-in 500ms;

    .emp-card-header {
      display: flex;

      .option-button {
        display: flex;
        align-items: center;
        cursor: pointer;
        gap: 2px;
      }
    }

    > img {
      margin-left: auto;
      margin-right: auto;
      object-fit: cover;
      border-radius: 100%;
      width: 70px;
      aspect-ratio: 1/1;
    }

    > h1 {
      font-weight: 700;
      font-size: 1.1rem;
      text-align: center;
      color: #0f2827;
    }

    > h2 {
      text-align: center;
      color: #b9bfc6;
      margin-bottom: .5rem;
    }

    color: #0f2827;

    .emp-card-body {
      background-color: #f2f8fd;
      border-radius: 4px; 
      padding: .5rem;
      display: grid;
      grid-template-columns: repeat(2, 1fr);

      .details {
        h3 {
          font-size: .6rem;
          font-weight: 600;
          line-height: 1.3rem;
          color: #a9b1bc;;
        }

        h2 {
          font-size: .8rem;
        }
      }
      .contact {
        margin-top: 1rem;
        grid-column: span 2;

        .row {
          display: flex;
          align-items: center;
          gap: .5rem;

          h2 {
            font-size: .8rem;
            line-height: 1.3rem;
          }
        }
      }
    }
  }

  @media (min-width: 320px) and (max-width: 812px) {
    .emp-card {
      padding: 1rem;
    }
  }

</style>