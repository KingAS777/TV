<template>
    <div class="container">
        <div class="row">
            <div class="col-8">
                <TheTV>
                    <video v-if="isTvOn" :src="source" autoplay playsinline></video>
                </TheTV>
            </div>
            <div class="col-4">
                <RemoteControl
                    @on-off-tv="onOffTv"
                    @next-channel="nextChannel"
                    @prev-channel="prevChannel"
                    @mute="mute"
                    @volume-down="volumeDown"
                    @volume-up="volumeUp"
                ></RemoteControl>
            </div>
        </div>
        <div>
            <h1 v-if="isTvOn" class="text-center">{{ playing }}</h1>
        </div>
    </div>
</template>

<script>
import TheTV from "./compotents/TheTV.vue";
import RemoteControl from "./compotents/RemoteControl.vue";

export default {
    components: {
        TheTV,
        RemoteControl,
    },
    data() {
        return {
            isTvOn: false,
            playing: null,
            muted: false,
            volume: 1.0,
            channels: ["1+1", "Novyy Channel", "Sport", "Pixel"],
            mapChannelsToSource: {
                "1+1": "http://127.0.0.1:8000/src/videos/kvartal95.mp4",
                "Novyy Channel": "http://127.0.0.1:8000/src/videos/noviy.mp4",
                Sport: "http://127.0.0.1:8000/src/videos/sport.mp4",
                Pixel: "http://127.0.0.1:8000/src/videos/pixel.mp4",
            },
        };
    },
    computed: {
        source() {
            if (this.playing) {
                return this.mapChannelsToSource[this.playing];
            }
            return null;
        },
    },
    methods: {
        onOffTv() {
            if (!this.isTvOn) {
                this.isTvOn = true;
                if (!this.playing) {
                    this.playing = this.channels[0];
                }
                this.playingSource = this.mapChannelsToSource[this.playing];
            } else {
                this.isTvOn = false;
            }
        },
        nextChannel() {
            if (!this.isTvOn) {
                return;
            }
            const currentIndex = this.channels.findIndex((elem) => this.playing === elem);
            let nextIndex = currentIndex + 1;
            if (currentIndex === this.channels.length - 1) {
                nextIndex = 0;
            }
            this.playing = this.channels[nextIndex];
        },
        prevChannel() {
            if (!this.isTvOn) {
                return;
            }
            const currentIndex = this.channels.findIndex((elem) => this.playing === elem);
            let prevIndex = currentIndex - 1;
            if (currentIndex === 0) {
                prevIndex = this.channels.length - 1;
            }
            this.playing = this.channels[prevIndex];
        },
        mute() {
            const video = document.querySelector("video");
            this.muted = !this.muted;
            video.muted = this.muted;
        },
        volumeDown() {
            this.volume = this.volume - 0.1;
            if (this.volume < 0) {
                this.volume = 0;
            }
            this.setVolume(this.volume);
        },
        volumeUp() {
            this.volume = this.volume + 0.1;
            if (this.volume > 1) {
                this.volume = 1;
            }
            this.setVolume(this.volume);
        },
        setVolume(volume) {
            const video = document.querySelector("video");
            video.volume = volume;
        },
    },
};
</script>

<style>
video {
    width: 100%;
    height: auto;
}
</style>
