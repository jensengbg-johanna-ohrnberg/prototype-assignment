<template>
  <div class="wrapper">
      <nav>
        <button class="first-aid-button" @click="goToFirstAid">
          <img src="../assets/AID.svg" alt="">
          First Aid
        </button>
      </nav>
      <section class="content">
        <h1>Pick Up</h1>
        <p class="info">Check all that applies to the patient</p>
        <ul>
          <li v-for="status in medicalStatus" :key="status.name">
            <HealthState :status="status.lable" :description="status.description"/>
          </li>
        </ul>
      </section>
      <primaryButton :text="'send'" @click="goToDropOff" />
  </div>
</template>

<script>
import HealthState from '@/components/HealthState.vue';
import primaryButton from '../components/globalComp/primaryButton.vue'
export default {
  components: {
    HealthState,
    primaryButton
  },
  data: () => {
    return {
      medicalStatus: [
        {
          lable: "Pre-eclampsia",
          description: "Patient shows sign of pre-eclampsia"
        },
        {
          lable: "Sever bleeding",
          description: "Patient is bleeding at time of pick up"
        },
        {
          lable: "Severe pain",
          description: "Patient has severe pain"
        }
      ]
    }
  },
  methods: {
    goToDropOff() {
      this.$router.push({ path: 'dropoff' });
    },
    goToFirstAid() {
      this.$router.push({ path: 'firstaid' });
    }
  }
}
</script>

<style lang="scss" scoped>
  .wrapper {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    padding: 2rem 1.5rem;
    background: #ffffff;

    nav {
      width: 100%;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: flex-end;

      .first-aid-button {
        background: $primary;
        @include centeredFlex();
        flex-direction: column;
        width: 4.8rem;
        height: 4.8rem;
        border-radius: 50%;
        color: #ffffff;
        font-weight: 900;
        text-transform: uppercase;
        font-size: .6rem;
        box-shadow: $buttonShadow;
        border: none;

        img {
          margin-bottom: .4rem;
        }
      }
    }

    .content {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;

      h1 {
        align-self: center;
        @include headingLarge();
      }

      .info {
        color: #888;
        font-size: 1.1rem;
      }

      ul {
        width: 100%;
        list-style: none;
      }
    }
}
</style>
