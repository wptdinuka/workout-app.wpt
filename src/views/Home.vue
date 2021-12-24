
<template>
  <div class="container">
    <h1 class="title">Welcome to WorkOut.App.wpt</h1>
   <div class="main-section">
     <a href="Create">
       <img
          src="@/assets/images/a2.jpg"
          class="img1"
          alt=""
        />
     </a>
     <a href="Workout-List">
       <img
          src="@/assets/images/a1.jpg"
          class="img2"
          alt=""
        />
     </a>
   </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { supabase } from "../supabase/init";
export default {
  name: "home",
  components: {},
  setup() {
    // Create data / vars
    const data = ref([]);
    const dataLoaded = ref(null);
    // Get data
    const getData = async () => {
      try {
        const { data: workouts, error } = await supabase.from("workouts").select("*");
        if (error) throw error;
        data.value = workouts;
        dataLoaded.value = true;
      } catch (error) {
        console.warn(error.message);
      }
    };
    // Run data function
    getData();
    return { data, dataLoaded };
  },
};
</script>

<style scoped>

.img1,
.img2{
  height: 350px;
  width: 350px;
  margin: 60px;

}



.main-section{
  display: flex;
  flex-direction: row;
  background-color: gray;
}

.container {
 width: 70%;
 min-block-size: calc(100vh-70px);
}

.title {
  text-align: center;
  font-size: 3rem;
  font-weight: 500;
  margin: 40px 0px;
  border: 3px black solid;
}
</style>