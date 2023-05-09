<template>
  <header>
    <ul class="gnb">
      <!--  v-값,i-속성명 -->
      <!-- sdata가 업데이트가 아니라. 스토어가 있는 데이터가 업데이트라서 직접적으로 적어주어야 한다.  -->
      <!-- 리액티브 데이터인  뷰엑스 스토어 cityData 변수를 
      컴포넌트 변수인 sdata 에 할당하여 사용하면 처음에만 할당된 변수로 세팅이 되고, 
    cityData 가 변경될 때 반영되지 않는다.!!
  따라서 리액티브 데이터를 직접 해당자리에 사용해야 한다.!!  -->
      <!-- <li v-for="(v, i) in sdata"  v-bind:key="i" v-if="i != '인트로'" >-->
      <li
        v-for="(v, i) in this.$store.state.cityData"
        v-bind:key="i"
        v-if="i != '인트로'"
      >
        <a href="#" v-on:click="chgData(i)">
          {{ i }}
        </a>
      </li>
    </ul>
    <!-- 메뉴선택이동링크 -->
    <div class="m2">
      <a href="#" v-on:click="chgMenu(num)" v-text="'메뉴' + num"></a>
    </div>
  </header>
</template>

<script>
export default {
  name: "TopArea",
  data() {
    return {
      // 1. 도시정보 객체 변수

      sdata: this.$store.state.cityData,
      // 2. 메뉴번호(처음에 다음메뉴인 2번 넣음 )
      num: 2
    };
  },
  methods: {
    // 스토어 변수 업데이트 메서드
    chgData(pm) {
      console.log("업데이트!", pm);
      // 뮤테이션 메서드 호출하기!
      this.$store.commit("chgData", pm);
    },
    // 메뉴변경하기 메서드
    chgMenu(n) {
      // n - 메뉴번호전달
      console.log("메뉴변경:", n);
      // 뮤테이션 메서드 호출하기!
      this.$store.commit("chgMenu", n);

      // 메뉴1/ 메뉴2 전환을 위한 변수변경하기
      // 컴포넌트 변수인 num 을 변경한다.!!!
      n == 1 ? (this.num = 2) : (this.num = 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.m2 {
  display: block;
  text-align: right;
}
.m2 a {
  font-size: 20px;
}
.m2 a:hover {
  text-decoration: underline;
  text-decoration-style: double;
  color: green;
}

header {
  padding: 15px;
  border: 2px solid #ccc;
}
header ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  justify-content: center;
  gap: 0 15px;
}
header a {
  font-size: 30px;
  color: #222;
  text-decoration: none;
}
header a:hover,
header a.on {
  color: orangered;
  text-decoration: overline;
  text-decoration-style: wavy;
}
</style>
