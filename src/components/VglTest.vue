<template>
  <v-container fluid>
    <v-row>
      <v-col cols="3">
        <VglOptions v-model="vglOptions" />
      </v-col>

      <v-col cols="9">
        <vgl-renderer
          id="vgl-canvas"
          :antialias="vglOptions.antialias"
          :alpha="vglOptions.alpha"
          :disable-premultiplied-alpha="!vglOptions.premultipliedAlpha"
          :disable-depth="!vglOptions.depth"
          :precision="vglOptions.precision"
          :disable-stencil="!vglOptions.stencil"
          :preserve-drawing-buffer="vglOptions.preserveDrawingBuffer"
          :shadow-map-enabled="vglOptions.shadowMapEnabled"
          :logarithmic-depth-buffer="vglOptions.logarithmicDepthBuffer"
          camera="camera"
          scene="scene"
        >
          <vgl-scene
            name="scene"
            :background-color="vglOptions.backgroundColor"
          >
            <vgl-camera-helper
              v-if="vglOptions.cameraHelper"
              camera="camera"
            />
            <vgl-axes-helper
              v-if="vglOptions.axesHelper"
              :size="vglOptions.axesSize"
            />
            <!--<vgl-obj-loader src="/seahorse.obj" />-->
            <vgl-box-geometry name="box" />
            <vgl-ambient-light intensity="0.5" />
            <vgl-directional-light
              position="1 1 1"
              intensity="0.5"
            />
          </vgl-scene>
          <vgl-perspective-camera
            name="camera"
            orbit-position="300 1 0.2"
            orbit-target="0 0 -300"
          />
        </vgl-renderer>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
import VglOptions from '@/components/VglOptions'
// import VglObjLoader from '@/components/VglObjLoader'

export default {
  name: 'HelloWorld',
  components: {
    // VglObjLoader,
    VglOptions,
  },
  data: () => ({
    board: null,
    loading: true,
    vglOptions: {},
  }),
  mounted () {
    axios
      .get('http://localhost:8001/board')
      .then(res => {
        console.log(res.data)
        this.board = res.data
      })
      .catch(err => {
        console.error(err)
      })
      .finally(() => {
        this.loading = false
      })
  },
}
</script>

<style scoped lang="sass">
#vgl-canvas
  height: 800px
  width:  800px
</style>
