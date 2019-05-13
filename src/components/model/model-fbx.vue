<script>
import { OBJLoader } from './loaders/OBJLoader'
import { toIndexed } from './util'
let FBXLoader = require('three-fbxloader-offical')
import mixin from './model-mixin.vue'

import * as THREE from 'three'
import { getSize, getCenter } from './util'

export default {
    name: 'model-obj',
    mixins: [ mixin ],
    props: {
        lights: {
            type: Array,
            default() {
                return [
                    {
                        type: 'HemisphereLight',
                        position: { x: 0, y: 1, z: 0 },
                        skyColor: 0xaaaaff,
                        groundColor: 0x806060,
                        intensity: 0.2
                    },
                    {
                        type: 'DirectionalLight',
                        position: { x: 1, y: 1, z: 1 },
                        color: 0xffffff,
                        intensity: 0.8
                    }
                ]
            }
        },
        smoothing: {
            type: Boolean,
            default: false
        },
        mtlPath: {
            type: String
        },
        mtl: {
            type: String
        }
    },
    data() {
        return {
            loader: new OBJLoader(),
        }
    },
    watch: {
        mtl() {
            this.load();
        }
    },
    methods: {
        process( object ) {
            if ( this.smoothing ) {
                object.traverse( child => {
                    if ( child.geometry ) {
                        child.geometry = toIndexed( child.geometry );
                        child.geometry.computeVertexNormals();
                    }
                } )
            }
        },
        load() {

            if ( !this.src ) return;

            if ( this.object ) {
                this.wrapper.remove( this.object );
            }

            const onLoad = object => {

                if ( this.process ) {
                    this.process( object );
                }

                this.addObject( object )

                this.$emit( 'on-load' );

            }

            const onProgress = xhr => {

                this.$emit( 'on-progress', xhr );

            }

            const onError = err => {

                this.$emit( 'on-error', err );

            }

            this.loader.load( this.src, onLoad, onProgress, onError );

        },
    }
}
</script>
