<script>
import { initializeApp } from "firebase/app";
import {
  getFirestore,
  collection,
  doc,
  addDoc,
  getDocs,
  deleteDoc,
} from "firebase/firestore";

const firebaseConfig = {
  apiKey: "AIzaSyA1uh6C04jDSJzkF7lPSOe4_MnmpfrgJdY",
  authDomain: "userlog803.firebaseapp.com",
  databaseURL:
    "https://userlog803-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "userlog803",
  storageBucket: "userlog803.appspot.com",
  messagingSenderId: "219849884017",
  appId: "1:219849884017:web:818a28f6f94362a83136d0",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

export default {
  data() {
    return {
      keyId: "",
      fullname: "",
      note: "",
      userList: null,
    };
  },
  async created() {
    this.loadRecords();
  },
  methods: {
    async addRecord() {
      try {
        const docRef = await addDoc(collection(db, "users"), {
          key_id: this.keyId,
          fullname: this.fullname,
          note: this.note,
          created_time: Date.now(),
        });
        console.log("Document written with ID: ", docRef.id);
        this.loadRecords();
        // Clear form
        this.keyId = "";
        this.fullname = "";
        this.note = "";
      } catch (e) {
        console.error("Error adding document: ", e);
      }
    },
    async loadRecords() {
      const usersCol = collection(db, "users");
      const usersSnapshot = await getDocs(usersCol);
      this.userList = usersSnapshot.docs.map((doc) => [doc.id, doc.data()]);
      // console.log(usersSnapshot.docs);
      // console.log(this.userList);
    },
    async deleteRecord(docId) {
      await deleteDoc(doc(db, "users", docId));
      this.loadRecords();
    },
    showDate(timestamp) {
      return new Date(timestamp).toLocaleDateString("en-US");
    }
  },
};
</script>

<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"/>
  <div class="container">
    <header>
      <p>Nhập dữ liệu mới:</p>
      <input
        class="form-control"
        type="number"
        v-model="keyId"
        placeholder="Key ID"
      />
      <br />
      <input
        class="form-control"
        type="text"
        v-model="fullname"
        placeholder="Họ tên"
      />
      <br />
      <input
        class="form-control"
        type="text"
        v-model="note"
        placeholder="Ghi chú"
      />
      <br />
      <button class="btn btn-primary" @click="addRecord">Submit</button>
    </header>

    <br />
    <p>Danh sách khóa đã tạo:</p>
    <table class="table table-sm table-striped table-bordered">
      <thead>
        <tr>
          <th>Key ID</th>
          <th>Họ tên</th>
          <th>Ngày tạo</th>
          <th>Ghi chú</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in userList" :key="user[0]">
          <td>{{ user[1].key_id }}</td>
          <td>{{ user[1].fullname }}</td>
          <td>{{ showDate(user[1].created_time) }}</td>
          <td>{{ user[1].note }}</td>
          <td><button @click="deleteRecord(user[0])"><i class="fa fa-trash" /></button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
