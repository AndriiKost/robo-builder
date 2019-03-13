<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <div class="robot-name">
          {{ selectedRobot.head.title }}
          <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
        </div>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectPrevHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm"/>
        <button @click="selectPrevLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="left arm"/>
        <button @click="selectPrevTorsos()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorsos()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="left arm"/>
        <button @click="selectPrevRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="left arm"/>
        <button @click="selectPrevBases()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBases()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from '../../data/parts.js';

// helpers
function getPrevValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

function getNextValidIndex(index, length) {
  const incrementIndex = index + 1;
  return incrementIndex > length -1 ? 0 : incrementIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      selectHeadIndex: 0,
      selectLeftArmIndex: 0,
      selectTorsosIndex: 0,
      selectRightArmIndex: 0,
      selectBasesIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectHeadIndex],
        torso: availableParts.torsos[this.selectTorsosIndex],
        leftArm: availableParts.arms[this.selectLeftArmIndex],
        rightArm: availableParts.arms[this.selectRightArmIndex],
        base: availableParts.bases[this.selectBasesIndex],
      }
    }
  },
  methods: {
    selectNextHead() {
      this.selectHeadIndex = getNextValidIndex(this.selectHeadIndex, availableParts.heads.length)
    },
    selectPrevHead() {
      this.selectHeadIndex = getPrevValidIndex(this.selectHeadIndex, availableParts.heads.length)
    },
    selectNextLeftArm() {
      this.selectLeftArmIndex = getNextValidIndex(this.selectLeftArmIndex, availableParts.arms.length)
    },
    selectPrevLeftArm() {
      this.selectLeftArmIndex = getPrevValidIndex(this.selectLeftArmIndex, availableParts.arms.length)
    },
    selectNextRightArm() {
      this.selectRightArmIndex = getNextValidIndex(this.selectRightArmIndex, availableParts.arms.length)
    },
    selectPrevRightArm() {
      this.selectRightArmIndex = getPrevValidIndex(this.selectRightArmIndex, availableParts.arms.length)
    },
    selectNextTorsos() {
      this.selectTorsosIndex = getNextValidIndex(this.selectTorsosIndex, availableParts.torsos.length)
    },
    selectPrevTorsos() {
      this.selectTorsosIndex = getPrevValidIndex(this.selectTorsosIndex, availableParts.torsos.length)
    },
    selectNextBases() {
      this.selectBasesIndex = getNextValidIndex(this.selectBasesIndex, availableParts.bases.length)
    },
    selectPrevBases() {
      this.selectBasesIndex = getPrevValidIndex(this.selectBasesIndex, availableParts.bases.length)
    }
  }
}
</script>

<style>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  color: red;
}
</style>
