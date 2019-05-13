<template>
    <my-page title="3D 模型查看">
        <div class="common-container container">
            <div class="preview-box">
                <!-- <model-obj
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :mtl="mtlSrc"
                    :src="modelSrc" v-if="type === 'obj'"></model-obj> -->
                <!-- <model-ply src="/static/models/ply/binary/Lucy100k.ply"></model-ply> -->
                <!-- <model-ply src="/static/models/ply/6666.ply"></model-ply> -->
                <model-json
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :mtl="mtlSrc"
                    :src="modelSrc" v-if="type === 'json'"></model-json>
                <model-obj
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :mtl="mtlSrc"
                    :src="modelSrc" v-if="type === 'obj'"></model-obj>
                <model-ply
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :src="modelSrc" v-if="type === 'ply'"></model-ply>
                <model-fbx
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :mtl="mtlSrc"
                    :src="modelSrc" v-if="type === 'fbx'"></model-fbx>
                <!-- <model-collada src="static/models/collada/avatar.dae"></model-collada> -->
                <model-stl
                    :width="500"
                    :height="500"
                    :backgroundAlpha="bgAlpha"
                    :backgroundColor="bgColor"
                    :src="modelSrc" v-if="type === 'stl'"></model-stl>
            </div>
            <div class="tool-box">
                <div class="background-buttons">
                    <p>上传文件</p>
                    <input type="file" value="" @change="onFileChange($event)">
                    <!-- <button @click="bgAlpha = 0"></button> -->
                    <p>背景色</p>
                    <button @click="bgColor = '#ff0'">#ff0</button>
                    <button @click="bgColor = '#f00'">#f00</button>
                    <button @click="bgColor = '#13ce66'">#13ce66</button>
                    <p>透明度</p>
                    <button @click="bgAlpha = 0.5">0.5</button>
                    <button @click="bgAlpha = 1">1</button>
                    <button @click="bgAlpha = 0">0</button>
                </div>
            </div>
        </div>
    </my-page>
</template>

<script>
    import { ModelObj, ModelStl, ModelCollada, ModelFbx, ModelPly, ModelJson } from '../components/model'

    export default {
        data () {
            return {
                type: 'fbx',
                // type: 'stl',
                // modelSrc: '',
                // modelSrc: '/static/models/fbx/test.fbx',
                // mtlSrc: '/static/models/obj/88888.mtl',
                // modelSrc: '/static/models/obj/tree.obj',
                // modelSrc: '/static/models/stl/gear.stl',
                bgColor: '#ff0',
                bgAlpha: 0.5,
                page: {
                    menu: [
                        {
                            type: 'icon',
                            icon: 'help',
                            to: '/help'
                        }
                    ]
                }
            }
        },
        mounted() {
            let data = this.$route.query.data
            if (data) {
                this.modelSrc = data
                let arr = data.split('.')
                this.type = arr[arr.length - 1]
                console.log(this.type)
            }
        },
        methods: {
            onFileChange(e) {
                let files = e.target.files
                let file = files[0]
                if (!file) {
                    return
                }
                let arr = file.name.split('.')
                this.type = arr[arr.length - 1]
                console.log('file', file)
                console.log('this.type', this.type)
                this.modelSrc = window.URL.createObjectURL(file)
            },
        },
        components: {
            ModelObj,
            ModelStl,
            ModelCollada,
            ModelFbx,
            ModelPly,
            ModelJson,
        }
    }
</script>

<style lang="scss" scoped>
.container {
    display: flex;
    flex-wrap: wrap;
}
.preview-box {
    // position: absolute;
    // top: 0;
    // left: 0;
    // right: 256px;
    // bottom: 0;
    padding: 16px;
}
.tool-box {
    // position: absolute;
    // top: 0;
    // right: 0;
    // bottom: 0;
    width: 256px;
}
</style>
