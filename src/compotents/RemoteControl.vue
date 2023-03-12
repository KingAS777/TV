<template>
    <div class="container mt-5">
        <div class="row remote">
            <div class="button-row d-flex pt-2">
                <div class="col-4">
                    <button @click="$emit('mute')" class="btn">
                        <img src="../assets/mute.png" alt="" />
                    </button>
                </div>
                <div class="col-4"></div>
                <div class="col-4">
                    <button @click="$emit('on-off-tv')" class="btn">
                        <img src="../assets/power.png" alt="" />
                    </button>
                </div>
            </div>
            <div class="button-row d-flex">
                <div class="col-4"></div>
                <div class="col-4">
                    <button @click="$emit('prev-channel')" class="btn">
                        <img class="top-arrow" src="../assets/arrow.png" alt="" />
                    </button>
                </div>
                <div class="col-4"></div>
            </div>
            <div class="button-row d-flex">
                <div class="col-4">
                    <button @click="$emit('volume-down')" class="btn btn-outline">
                        <img src="../assets/arrow.png" alt="" />
                    </button>
                </div>
                <div class="col-4"></div>
                <div class="col-4">
                    <button @click="$emit('volume-up')" class="btn">
                        <img class="right-arrow" src="../assets/arrow.png" alt="" />
                    </button>
                </div>
            </div>
            <div class="button-row d-flex">
                <div class="col-4"></div>
                <div class="col-4">
                    <button @click="$emit('next-channel')" class="btn">
                        <img class="bottom-arrow" src="../assets/arrow.png" alt="" />
                    </button>
                </div>
                <div class="col-4"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    emits: ["on-off-tv", "next-channel", "prev-channel", "mute", "volume-up", "volume-down"],
};
</script>

<style scoped>
.remote {
    background: #888;
    width: 60%;
    height: 300px;
    border-radius: 5%;
    border: 4px solid black;
}

img {
    width: 40px;
}

.top-arrow {
    rotate: 90deg;
}

.right-arrow {
    rotate: 180deg;
}

.bottom-arrow {
    rotate: 270deg;
}
</style>
