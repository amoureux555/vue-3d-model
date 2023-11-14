<template>
  <demo-block :vue-code="code" :html-code="htmlCode">
    <template slot="preview">
      <model-fbx
        :backgroundAlpha="0"
        :rotation="rotation"
        @on-load="onLoad"
        @on-error="onError"
        src="static/models/fbx/住建大厦高1.fbx"
      ></model-fbx>
      <div class="example-loading" v-show="loading"></div>
    </template>
    <!-- <template slot="preview">
      <model-fbx
        :backgroundAlpha="0"
        @on-load="onLoad"
        @on-error="onError"
        src="static/models/公交站台.fbx"
      ></model-fbx>
      <div class="example-loading" v-show="loading"></div>
    </template> -->
  </demo-block>
</template>

<script>
import DemoBlock from "../components/demo-block.vue";
import ModelFbx from "../../src/model-fbx.vue";

const code = `
<template>
    <model-obj src="static/models/fbx/住建大厦高1.fbx"></model-obj>
    <model-obj src="static/models/fbx/公交站台.fbx"></model-obj>
</template>

<script>
    import { modelFbx } from 'vue-3d-model'

    export default {
        components: {
            ModelFbx
        }
    }
<\/script>
`;

const htmlCode = `
<body>
    <div id="app">
        <model-fbx src="static/models/fbx/住建大厦高1.fbx"></model-fbx>
        <model-fbx src="static/models/fbx/公交站台.fbx"></model-fbx>
    </div>
    #scripts#
    <script>
        new Vue({
            el: '#app'
        })
    <\/script>
</body>
`;

export default {
  name: "demo-focus",
  data() {
    return {
      code,
      htmlCode,
      loading: true,
      rotation: {
        x: -1.5,// 在模型的方向 | 远近
        y: 0, // 控制模型往哪个方向倒
        z: 100,
      },
    };
  },
  methods: {
    onLoad() {
      this.loading = false;
      // this.rotate();
    },
    onError(e) {
      console.error(e);
    },
    rotate() {
      requestAnimationFrame(this.rotate);
      this.rotation.z += 0.01;
    },
  },
  components: {
    ModelFbx,
    DemoBlock,
  },
};
</script>
