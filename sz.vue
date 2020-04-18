<template>
  <div>
    <div class="photo">
      <div class="oll">
        <img :src="base64" v-show="base64!='../../assets/biyezheng.png'">
      </div>
      <input type="file" name="file" ref="files" accept="image/*" @change="uploadImg" class="iipp">
    </div>
  </div>
</template>

<script>
import Clipic from "clipic";
const clipic = new Clipic();
export default {
  components: {},
  data() {
    return {
      base64: "../../assets/biyezheng.png",
      zc: [
        "请选择",
        "一年级",
        "二年级",
        "三年级",
        "四年级",
        "五年级",
        "六年级",
        "七年级",
        "八年级",
        "九年级"
      ],
      ktime: ["2020.2.3", "2020.2.3", "2020.2.3"],
      jtime: ["2020.5.5", "2020.5.5", "2020.5.5"],
      op: true,
      tdb: false
    };
  },
  mounted() {
    this.a = document.getElementById("pd-doot");
  },
  methods: {
    uploadImg() {
      let _this = this;
      const files = this.$refs.files.files;
      const reader = new FileReader();
      reader.readAsDataURL(files[0]);
      reader.onload = img => {
        clipic.getImage({
          width: 500,
          height: 500,
          src: img.target.result,
          onDone: base64 => {
            //这里就是上传完成的回调函数，可以在这里请求接口上传至服务器
            _this.base64 = base64;
            console.log(this.base64); //图片上传完成后生成的base64
          }
        });
      };
      //执行完成之后把input的value值置空，否则无法选择相同的图片
      this.$refs.files.value = "";
    },
    cd() {
      location.href = "#/pd";
    },
    dc() {
      location.href = "#/zhic";
    }
  }
};
</script>

<style>
.photo{
  font-size: 0.3rem;
}
</style>
