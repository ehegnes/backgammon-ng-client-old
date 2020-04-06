<template>
  <v-card>
    <v-card-text>
      <div class="caption mb-4">
        SCENE
      </div>
      <!-- TODO: Enforce pressing enter to confirm change -->
      <v-text-field
        v-model="value.backgroundColor"
        label="Background color"
        outlined
      />

      <div class="caption">
        RENDERER
      </div>
      <v-checkbox
        v-model="value.antialias"
        label="Antialias"
      />
      <v-checkbox
        v-model="value.alpha"
        label="Alpha"
      />
      <v-checkbox
        v-model="value.premultipliedAlpha"
        label="Premultiplied alpha"
      />
      <v-checkbox
        v-model="value.depth"
        label="Depth buffer"
      />
      <v-checkbox
        v-model="value.stencil"
        label="Stencil buffer"
      />
      <v-checkbox
        v-model="value.preserveDrawingBuffer"
        label="Preserve drawing buffer"
      />
      <v-checkbox
        v-model="value.logarithmicDepthBuffer"
        label="Logarithmic depth buffer"
      />
      <v-checkbox
        v-model="value.shadowMapEnabled"
        label="Shadow map"
      />
      <v-select
        v-model="value.precision"
        :items="precisionItems"
        label="Precision"
      />

      <div class="caption">
        HELPERS
      </div>
      <v-checkbox
        v-model="value.cameraHelper"
        label="Camera"
      />
      <v-checkbox
        v-model="value.axesHelper"
        label="Axes"
      />
      <v-slider
        v-if="value.axesHelper"
        v-model="value.axesSize"
        label="Axes Size"
        thumb-label
      />
    </v-card-text>
  </v-card>
</template>

<script>

const value = {
  cameraHelper: false,
  axesHelper: true,
  axesSize: 1,
  antialias: true,
  backgroundColor: '#000',
  alpha: false,
  premultipliedAlpha: true,
  depth: true,
  precision: 'highp',
  stencil: true,
  preserveDrawingBuffer: false,
  shadowMapEnabled: false,
  logarithmicDepthBuffer: false,
}
export default {
  data: () => ({
    value,
    precisionItems: ['highp', 'mediump', 'lowp'],
  }),
  watch: {
    value: {
      deep: true,
      handler () {
        this.$emit('input', this.value)
      },
    },
  },
  mounted () {
    // Force initial default value, regardless of the parent's `v-model` value.
    this.$emit('input', value)
  },
}
</script>
