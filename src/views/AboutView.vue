<script>
// import axios from "axios";

// import { initializeApp } from "firebase/app";
// import { getFirestore, collection, getDocs } from "firebase/firestore/lite";
// import { getFirestore, collection, addDoc } from "firebase/firestore"; 

// const firebaseConfig = {
//   apiKey: "AIzaSyA1uh6C04jDSJzkF7lPSOe4_MnmpfrgJdY",
//   authDomain: "userlog803.firebaseapp.com",
//   databaseURL:
//     "https://userlog803-default-rtdb.asia-southeast1.firebasedatabase.app",
//   projectId: "userlog803",
//   storageBucket: "userlog803.appspot.com",
//   messagingSenderId: "219849884017",
//   appId: "1:219849884017:web:818a28f6f94362a83136d0",
// };

// Initialize Firebase
// const app = initializeApp(firebaseConfig);
// const db = getFirestore(app);

// const keysCol = collection(db, "keys");
// const keySnapshot = await getDocs(keysCol);
// const keyList = keySnapshot.docs.map((doc) => doc.data());
// console.log(keyList);

// try {
//   const docRef = await addDoc(collection(db, "users"), {
//     first: "Ada",
//     last: "Lovelace",
//     born: 1815,
//   });
//   console.log("Document written with ID: ", docRef.id);
// } catch (e) {
//   console.error("Error adding document: ", e);
// }

export default {
  data() {
    return {
      newKey: {
        type: 0,
        user: "",
      },
    };
  },
  created() {},
};
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
