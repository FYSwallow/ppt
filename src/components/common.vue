<template>
    <div class="common">
        <div class="onlyPic" v-if="msg.imagePath && !msg.description" :style ='{backgroundImage: "url(" + msg.imagePath + ")"}'>
            <h3>{{msg.topic}}</h3>
        </div>
        <div class="pic_text_noDes" v-if="msg.imagePath && msg.description && !msg.topic" :style ='{backgroundImage: "url(" + msg.imagePath + ")"}'>
            <p>{{msg.description}}</p>
        </div>
        <div class="pic_text_des" v-if="msg.imagePath && msg.description && msg.topic" :style ='{backgroundImage: "url(" + msg.imagePath + ")"}'>
            <h3>{{msg.topic}}</h3>
            <p>{{msg.description}}</p>
        </div>
        <div class="onlyText" v-if="!msg.imagePath && msg.description && !msg.videoPath">
            <h3>{{msg.topic}}</h3>
            <p>{{msg.description}}</p>
        </div>
        <div class="video" v-if="msg.videoPath" >
            <video :src="msg.videoPath" autoplay controls="controls"></video>
            <p v-if="msg.description">{{msg.description}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['msg'],
    created() {
        console.log(this.msg)
    }

}
</script>

<style lang="scss">
.common {
    width: 100%;
    height: 100%;
    overflow: hidden;
    div {
        width: 100%;
        height:100%;
        background-size: 200px 100%;
        background-repeat:  no-repeat;
        padding: 10px;
        p {
            font-size: 14px;
        }
        video {
            width: 100%;
            height: 80%;
        }
    }
}
</style>