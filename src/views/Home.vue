<template>
    <my-page title="3D 模型查看">
        <div class="preview-box">
            <model-obj
                :width="500"
                :height="500"
                :backgroundAlpha="bgAlpha"
                :backgroundColor="bgColor"
                :src="modelSrc" v-if="type === 'obj'"></model-obj>
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
    </my-page>
</template>

<script>
    import { ModelObj, ModelStl, ModelCollada } from 'vue-3d-model'

    export default {
        data () {
            return {
                type: 'obj',
                modelSrc: '',
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
        components: {
            ModelObj,
            ModelStl,
            ModelCollada
        }
    }
</script>

<style lang="scss" scoped>
.preview-box {
    position: absolute;
    top: 0;
    left: 0;
    right: 256px;
    bottom: 0;
    padding: 16px;
}
.tool-box {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    width: 256px;
}
</style>
