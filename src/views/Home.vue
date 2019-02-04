<template>
    <my-page title="3D 模型查看">
        <div class="preview-box">
            <model-obj
                :width="500"
                :height="500"
                :backgroundAlpha="bgAlpha"
                :backgroundColor="bgColor"
                src="/static/models/obj/tree.obj"></model-obj>
        </div>
        <div class="tool-box">
            <div class="background-buttons">
                <p>Color</p>
                <button @click="bgColor = '#ff0'">#ff0</button>
                <button @click="bgColor = '#f00'">#f00</button>
                <button @click="bgColor = '#13ce66'">#13ce66</button>
                <p>Alpha</p>
                <button @click="bgAlpha = 0.5">0.5</button>
                <button @click="bgAlpha = 1">1</button>
                <button @click="bgAlpha = 0">0</button>
            </div>
        </div>
    </my-page>
</template>

<script>
    import { ModelObj } from 'vue-3d-model'

    export default {
        data () {
            return {
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
        components: {
            ModelObj
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
