<template>
  <div id="app">
    <el-container style="min-height:100vh;width:100%">
      <el-header style="justify-content: center;height:auto;background:#509176">
        <Banner/>
      </el-header>

      <el-container class="main-wrap">
        <Aside></Aside>
        <el-container>
          <el-main id="main" style="box-shadow: 0px 0px 5px #cccccc;">
            <transition name="fade" mode="out-in">
              <router-view id="container"/>
            </transition>
          </el-main>
        </el-container>
      </el-container>

      <footer
        style="display:flex;flex-direction: column;justify-content: center;align-items:center"
      >
        <Marked style="text-align:center;display:flex;margin:0px;padding:0px;" :input="content"/>
        <div>
          <el-button
            @click="()=>{dialogFormVisible=true}"
            type="text"
          >ASIM2019 Copyright @ 2019-2020</el-button>
        </div>
        <!-- <span>ASIM2019 Copyright @ 2019-2020</span> -->
      </footer>
    </el-container>
    <el-dialog :visible.sync="dialogFormVisible" small>
      <el-form :model="form">
        <el-form-item label="密码" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="handlePassword">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import Aside from "@/components/Aside.vue";
import Banner from "@/components/Banner.vue";
import Marked from "@/components/Marked.vue";

export default {
  components: {
    Aside,
    Banner,
    Marked
  },
  data: function() {
    return {
      form: {
        name: ""
      },
      content: "",
      dialogFormVisible: false,
      formLabelWidth: "auto"
    };
  },
  methods: {
    handlePassword: function() {
      if (this.form.name === "Password") {
        this.$router.push("./admin");
        this.dialogFormVisible = false;
      }
    }
  },
  created: async function() {
    let res = await this.$request("post", `/util/detail`, {
      hash: "footer"
    });
    this.content = res.code == 1 ? res.data : "# Hello ASIM2019";
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.el-footer > * {
  font-size: 0.5rem;
  color: #444;
}

.el-footer > * :hover {
  text-decoration: none;
  color: #444;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#container {
  margin: 0px;
  padding: 0px;
}

.el-row {
  margin-bottom: 20px;
}

.el-row:last-child {
  margin-bottom: 0;
}

.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}

.el-header {
  /* background-color: #b3c0d1;
  color: #333; */
  padding: 0px !important;
  display: flex;
  /* line-height: 100px; */
  /* line-height: 100px; */
  justify-content: space-between;
  width: 100vw;
}

.el-header span {
  display: flex;
  align-items: flex-start;
}

.small_title {
  height: 40px;
  line-height: 40px;
  margin: 0;
  padding: 0%;
  font-size: 2rem;
}

.el-footer {
  /* background-color: #b3c0d1;
  color: #333; */
  display: flex;
  line-height: 20px;
  justify-content: space-around;
  width: 100vw;
}

.el-footer > * {
  align-items: stretch;
  text-align: center;
  margin: auto;
}

.main-wrap {
  width: 100%;
  max-width: 1280px;
  margin: auto;
}

.main-wrap > * {
  padding: 10px;
}

#main {
  padding-top: 0px;
}

.text {
  font-size: 14px;
}

a {
  text-decoration: none;
  color: #333;
}

a:hover {
  text-decoration: none;
  color: #509176;
}

a:visited {
  text-decoration: none;
}
</style>


