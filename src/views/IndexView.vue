<script>
import {defineComponent} from 'vue'
import {SorterGame, startDragNDrop} from "@/assets/sorter.js";
import CongratulationsMessage from "@/components/CongratulationsMessage.vue";

export default defineComponent({
    name: "IndexView",
    components: {CongratulationsMessage},
    data() {
        return {
            sorterGame: {},
        }
    },
    mounted() {
        this.sorterGame = new SorterGame(this.$refs.sorter)
        startDragNDrop(this.sorterGame)
    }
})
</script>

<template>
    <div class="sorter d-flex flex-column h-100 p-5" ref="sorter">

        <CongratulationsMessage v-if="sorterGame.success"/>

        <div class="drag-item sharp text d-flex align-items-center text-center" data-target="sharp">
            Знак альтерации, обозначающий повышение стоящих справа от него нот на один хроматический полутон.
        </div>

        <div class="drag-item flat text d-flex align-items-center text-center" data-target="flat">
            знак альтерации, обозначающий понижение стоящих справа от него нот на один хроматический полутон
        </div>

        <div class="drag-item natural text d-flex align-items-center text-center" data-target="natural">
            в музыкальной нотации знак альтерации, означающий отмену ранее назначенного бемоля или диеза для той ноты, перед которой он стоит. Действует до конца такта.
        </div>

        <div class="drag-item sharp img" data-target="sharp"></div>
        <div class="drag-item flat img" data-target="flat"></div>
        <div class="drag-item natural img" data-target="natural"></div>


        <div class="title text-center">
            Собери определения
        </div>
        <div class="d-flex game flex-column">
            <div class="d-flex flex-column h-100 w-100 mb-1">
                <div class="drag-container d-flex align-items-center w-100 m-1" id="sharp">
                    <div class="h1">
                        Диез
                    </div>
                </div>
                <div class="drag-container d-flex align-items-center w-100 m-1" id="flat">
                    <div class="h1 text-center">
                        Бемоль
                    </div>
                </div>
                <div class="drag-container d-flex align-items-center w-100 m-1" id="natural">
                    <div class="h1 text-center">
                        Бекар
                    </div>
                </div>
            </div>

        </div>

    </div>
</template>

<style scoped>
.drag-item {
    position: absolute;
    //width: 200px;
    height: 20vh;
    z-index: 10;
    background-size: contain;
    background-repeat: no-repeat;
    //background-color: black;
}


.text {
    height: 14vh;
    width: 50vw;
    font-size: 2rem;
    background-color: rgba(255, 255, 255, 0.95);
    border-radius: 1rem;
    border: 1px rgba(0, 0, 0, 0.85) solid;
}

.drag-container {
    width: 400px;
    height: calc(100%/3);
    background: rgba(255, 255, 255, 0.95);
    border-radius: 1rem;
}


.title {
    font-size: 4rem;
    font-weight: 700;
    background-size: 100% 140%;
    background-repeat: no-repeat;
    background-position-y: -10px;
    color: white;
}

.game {
    flex-grow: 1;
    height: 100%;
}

.img {
    background-size: contain;
    background-repeat: no-repeat;
    width: 15vw;
    height: 20vh;
}

.sharp.img {
    background-image: url("/public/assets/img/sharp.png");
    
}

.flat.img {
    background-image: url("/public/assets/img/flat.png");
}

.natural.img {
    background-image: url("/public/assets/img/natural.png");
}

.h1 {
    margin-left: 2vw;
    font-size: 3.5rem;
    z-index: 20;
}
</style>