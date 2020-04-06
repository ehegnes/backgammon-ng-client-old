// Copied directly from
// https://github.com/vue-gl/vue-gl/blob/744a986d51e5706246d815fa7403d915829447f4/examples/loaders/vgl-obj-loader.js
// because there is presumably no sane exportation of this component by the `vue-gl` folk...

<script>
import { OBJLoader2Parallel } from 'three/examples/jsm/loaders/OBJLoader2Parallel'
import { Object3D } from 'three'
import { VglObject3d } from 'vue-gl'

export default {
  mixins: [VglObject3d],
  props: {
    src: {
      required: true,
      type: String,
    },
  },
  computed: {
    inst () {
      const object = new Object3D()
      const loader = new OBJLoader2Parallel()
      loader.setBaseObject3d(object)
      loader.load(this.src, () => { this.vglObject3d.emit() })
      return object
    },
  },
}
</script>
