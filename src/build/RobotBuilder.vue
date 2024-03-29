<template>
      <div>
    <div class="top-row">
      <div class="top part">
        <div class="robot-name">
          {{ selectedRobot.head.title }}
        </div>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm"/>
        <button @click="selectPreviousLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="torso"/>
        <button @click="selectPreviousTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="right arm"/>
        <button @click="selectPreviousRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="base"/>
        <button @click="selectPreviousBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>

</template>

<script>
import availableParts from '../data/parts';

function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      selectedHeadIndex: 0,
      selectedLeftArmIndex: 0,
      selectedRightArmIndex: 0,
      selectedTorsoIndex: 0,
      selectedBaseIndex: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: this.availableParts.heads[this.selectedHeadIndex],
        leftArm: this.availableParts.arms[this.selectedLeftArmIndex],
        rightArm: this.availableParts.arms[this.selectedRightArmIndex],
        torso: this.availableParts.torsos[this.selectedTorsoIndex],
        base: this.availableParts.bases[this.selectedBaseIndex],
      };
    },
  },
  methods: {
    selectNextHead() {
      const totalHeads = this.availableParts.heads.length;
      this.selectedHeadIndex = getNextValidIndex(this.selectedHeadIndex, totalHeads);
    },
    selectPreviousHead() {
      const totalHeads = this.availableParts.heads.length;
      this.selectedHeadIndex = getPreviousValidIndex(this.selectedHeadIndex, totalHeads);
    },
    selectNextLeftArm() {
      const totalLeftArms = this.availableParts.arms.length;
      this.selectedLeftArmIndex = getNextValidIndex(this.selectedLeftArmIndex, totalLeftArms);
    },
    selectPreviousLeftArm() {
      const totalLeftArms = this.availableParts.arms.length;
      this.selectedLeftArmIndex = getPreviousValidIndex(this.selectedLeftArmIndex, totalLeftArms);
    },
    selectNextRightArm() {
      const totalRightArms = this.availableParts.arms.length;
      this.selectedRightArmIndex = getNextValidIndex(this.selectedRightArmIndex, totalRightArms);
    },
    selectPreviousRightArm() {
      const totalRArms = this.availableParts.arms.length;
      this.selectedRightArmIndex = getPreviousValidIndex(this.selectedRightArmIndex, totalRArms);
    },
    selectNextTorso() {
      const totalTorso = this.availableParts.torsos.length;
      this.selectedTorsoIndex = getNextValidIndex(this.selectedTorsoIndex, totalTorso);
    },
    selectPreviousTorso() {
      const totalTorso = this.availableParts.arms.length;
      this.selectedTorsoIndex = getPreviousValidIndex(this.selectedTorsoIndex, totalTorso);
    },
    selectNextBase() {
      const totalBase = this.availableParts.torsos.length;
      this.selectedBaseIndex = getNextValidIndex(this.selectedBaseIndex, totalBase);
    },
    selectPreviousBase() {
      const totalBase = this.availableParts.arms.length;
      this.selectedBaseIndex = getPreviousValidIndex(this.selectedBaseIndex, totalBase);
    },
  },
};

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

</style>
