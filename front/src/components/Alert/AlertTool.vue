<template>
  <div>
    <tr v-for="Data in AlertData" :key="Data.idx">
      <div class="w-[1600px]">
        <div
          class="flex p-4 mb-4 text-xl text-white-800 border border-red-300 rounded-lg bg-red-50 dark:bg-gray-800 dark:text-white dark:border-red-800"
          role="alert"
        >
          <svg
            class="flex-shrink-0 w-5 h-5"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z"
              clip-rule="evenodd"
            ></path>
          </svg>
          <div class="ml-3 text-xl font-bold">
            {{ Data.content }}
          </div>
          <button
            type="button"
            class="ml-auto -mx-1.5 -my-1.5 bg-red-50 text-white rounded-lg focus:ring-2 focus:ring-red-400 p-1.5 hover:bg-red-200 inline-flex h-8 w-8 dark:bg-gray-800 dark:text-white dark:hover:bg-gray-700"
            data-dismiss-target="#alert-border-2"
            @click="Close(Data.index)"
          >
            <svg
              aria-hidden="true"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </button>
        </div>
      </div>
    </tr>
  </div>
</template>

<script>
export default {
  name: "AlertTool",
  components: {},
  data: () => ({
    count: 3,
    AlertData: [],
  }),
  methods: {
    Close(contentindex) {
      //알람삭제
      this.$store.dispatch("deleteAlert", contentindex);
      this.changeLocalStorage();
    },
    changeLocalStorage() {
      const contentsArray = this.$store.getters.getAlertData; //index vuex -> 로컬스토리지 적용부분 1
      var contents = []; //index vuex -> 로컬스토리지 적용부분 2
      contentsArray.forEach(function (item) {
        //index vuex -> 로컬스토리지 적용부분 3
        contents.push(item["content"]);
      });
      localStorage.setItem("contents", contents); //index vuex -> 로컬스토리지 적용부분 4
    },
  },
  mounted() {
    this.AlertData = this.$store.getters.getAlertData;
  },
  computed: {
    changeAlertData: function () {
      return this.$store.getters.getAlertData;
    },
  },
  watch: {
    //vuex 변수의 값이 변함을 감지하는 곳
    changeAlertData(value) {
      this.AlertData = value;
    },
  },
};
</script>
