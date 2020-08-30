<template>
  <div class="hello" style="display: flex">
    <el-form ref="form" label-width="100px" size="small" style="width: 50%;margin-left: 20px;">
      <h2>进攻方属性</h2>
      <el-form-item label="速值">
        <el-input id="attackSpeed" placeholder="请输入内容" v-model="form.attackSpeed" style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="运值">
        <el-input id="attackLuk" placeholder="请输入内容" v-model="form.attackLuk" clearable style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="命中率">
        <el-input id="attackHit" placeholder="烙印+思念+技能（被动+升级）不包括战斗buff" v-model="form.attackHit" clearable
                  style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="技能基础命中">
        <el-input id="skillBaseHit" placeholder="右边表格没有的就填1" v-model="form.skillBaseHit" clearable
                  style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="Buff增幅">
        <el-input id="buffs" placeholder="1表示平BUFF" v-model="form.buffs" clearable style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="攻击次数">
        <el-input id="attackTimes" placeholder="多段技能次数 不是的话填1" v-model="form.attackTimes" clearable
                  style="width: 75%"></el-input>
      </el-form-item>
    </el-form>
    <el-form ref="form" label-width="100px" size="small" style="width: 50%;margin-left: 20px;">
      <h2>防守方属性</h2>
      <el-form-item label="速值">
        <el-input id="defenseSpeed" placeholder="请输入内容" v-model="form.defenseSpeed" clearable
                  style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="运值">
        <el-input id="defenseLuk" placeholder="请输入内容" v-model="form.defenseLuk" clearable style="width: 75%"></el-input>
      </el-form-item>
      <el-form-item label="回避率">
        <el-input id="defenseHit" placeholder="烙印+思念+技能（被动+升级）不包括战斗buff" v-model="form.defenseHit" clearable
                  style="width: 75%"></el-input>
      </el-form-item>
      <el-button type="primary" @click="calcFunction">计算</el-button>
      <ul>
        <li id="finalHit"></li>
        <br>
        <li id="aLotAttackNoHit"></li>
        <br>
        <li id="100Hit"></li>
        <br>
      </ul>
    </el-form>
    <div>
      <h2>非标准技能命中率</h2>
      <el-table :data="tableData.filter(data => !search || data.skillName.toLowerCase().includes(search.toLowerCase()))"
                style="width: 100%" height="300">
        <el-table-column prop="skillName" label="技能名" width="180"></el-table-column>
        <el-table-column prop="skillHit" label="命中率" width="180"></el-table-column>
        <el-table-column align="right" width="180">
          <template slot="header" slot-scope="scope">
            <el-input v-model="search" size="mini" placeholder="输入关键字搜索"/>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Dx2命中率计算器Beta',
      search: '',
      form: {
        attackSpeed: '',
        attackLuk: '',
        attackHit: '',
        defenseSpeed: '',
        defenseLuk: '',
        defenseHit: '',
        skillBaseHit: '',
        buffs: '',
        attackTimes: ''
      },
      tableData: [{
        skillName: '裂棘的魔槍',
        skillHit: '1.1'
      }, {
        skillName: '畢拉維德斬',
        skillHit: '0.9'
      }, {
        skillName: '猛毒之擊',
        skillHit: '0.9'
      }, {
        skillName: '鮮血到來',
        skillHit: '0.9'
      }, {
        skillName: '神威之擊',
        skillHit: '0.9'
      }, {
        skillName: '斬龍劍',
        skillHit: '0.9'
      }, {
        skillName: '天搖地動',
        skillHit: '0.9'
      }, {
        skillName: '殲滅外敵',
        skillHit: '0.9'
      }, {
        skillName: '巨人之戰',
        skillHit: '0.9'
      }, {
        skillName: '魔獸蛾摩拉召喚J',
        skillHit: '0.9'
      }, {
        skillName: '永恆之槍',
        skillHit: '1.3'
      }, {
        skillName: '冥界破',
        skillHit: '0.9'
      }, {
        skillName: '灼熱波浪',
        skillHit: '0.85'
      }, {
        skillName: '高天原之英勇',
        skillHit: '0.85'
      }, {
        skillName: '地獄兇爪',
        skillHit: '0.9'
      }, {
        skillName: '金剛發破/金剛發破L',
        skillHit: '0.9'
      }, {
        skillName: '突擊',
        skillHit: '0.95'
      }, {
        skillName: '狂亂硬爪',
        skillHit: '0.9'
      }, {
        skillName: '百萬噸重壓',
        skillHit: '0.85'
      }, {
        skillName: 'Million Stab',
        skillHit: '0.9'
      }, {
        skillName: '絕命鬥爭',
        skillHit: '0.95'
      }, {
        skillName: '橫斬',
        skillHit: '0.9'
      }, {
        skillName: '剎那五月雨擊',
        skillHit: '0.9'
      }, {
        skillName: '虛空爪激',
        skillHit: '0.9'
      }, {
        skillName: '鬼神樂',
        skillHit: '0.95'
      }, {
        skillName: '橫衝直撞',
        skillHit: '0.9'
      }, {
        skillName: '思念：火炮',
        skillHit: '0.9'
      }, {
        skillName: '五月雨斬',
        skillHit: '0.9'
      }, {
        skillName: '倫敦的恐懼',
        skillHit: '0.9'
      }, {
        skillName: '泰坦之戰',
        skillHit: '0.85'
      }, {
        skillName: '狂放一太刀',
        skillHit: '0.95'
      }, {
        skillName: '空間殺法',
        skillHit: '0.9'
      }, {
        skillName: '夜叉的凶爪',
        skillHit: '0.9'
      }, {
        skillName: '蛾摩拉的獄炎',
        skillHit: '0.9'
      }]
    }
  },
  methods: {
    calcFunction: function () {
      let attackSpeed = document.getElementById('attackSpeed').value
      let attackLuk = document.getElementById('attackLuk').value
      let attackHit = this.toPoint(document.getElementById('attackHit').value)
      let defenseSpeed = document.getElementById('defenseSpeed').value
      let defenseLuk = document.getElementById('defenseLuk').value
      let defenseHit = this.toPoint(document.getElementById('defenseHit').value)
      let skillBaseHit = document.getElementById('skillBaseHit').value
      let buffs = document.getElementById('buffs').value
      let attackTimes = document.getElementById('attackTimes').value

      let speedDiff = attackSpeed - defenseSpeed
      let lukDiff = attackLuk - defenseLuk
      let func1 = 0
      let func2 = 0
      let tempAcc = 0
      let minHit = 0
      let finalHit = 0
      let aLotAttackNoHit = 0
      let certainlyHit = 0

      if (speedDiff > 255) {
        func1 = 102
      } else {
        if (speedDiff < -60) {
          func1 = 76
        } else {
          if (speedDiff > -1) {
            func1 = 92 + 2 * Math.min(Math.floor(speedDiff / 10), 4)
          } else {
            func1 = 88 + 4 * Math.ceil((speedDiff / 20))
          }
        }
      }
      if (lukDiff > 255) {
        func2 = 13
      } else {
        if (lukDiff < -30) {
          func2 = -5
        } else {
          if (lukDiff > -1) {
            func2 = 5 + 2 * Math.min(Math.floor(lukDiff / 10), 3)
          } else {
            func2 = 0
          }
        }
      }
      let temp = (func1 + func2) / 100
      tempAcc = skillBaseHit * temp * buffs
      minHit = skillBaseHit * 0.2
      finalHit = Math.max(minHit, tempAcc + attackHit - defenseHit)
      aLotAttackNoHit = Math.min(Math.pow(finalHit, attackTimes), 1)
      certainlyHit = Math.max(0, Math.ceil((1 - tempAcc + defenseHit) * 100) / 100)

      console.log('func1:' + func1)
      console.log('func2:' + func2)
      console.log('skillBaseHit:' + skillBaseHit)
      console.log('buffs:' + buffs)
      console.log('speedDiff:' + speedDiff)
      console.log('lukDiff:' + lukDiff)
      console.log('tempAcc:' + tempAcc)
      console.log('finalHit:' + finalHit)
      console.log('aLotAttackNoHit:' + aLotAttackNoHit)
      console.log('certainlyHit:' + certainlyHit)
      document.getElementById('finalHit').innerHTML = '最终命中率 ：' + this.toPercent(finalHit)
      document.getElementById('aLotAttackNoHit').innerHTML = '多段攻击不会被闪避的几率 ：' + this.toPercent(aLotAttackNoHit)
      document.getElementById('100Hit').innerHTML = '达到100%命中需要的命中率 ：' + this.toPercent(certainlyHit)
    },
    toPoint: function (percent) {
      let str = percent.replace('%', '')
      str = str / 100
      return str
    },
    toPercent: function (point) {
      let percent = Number(point * 100).toFixed(1)
      percent += '%'
      return percent
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.transition-box {
  margin-bottom: 10px;
  width: 200px;
  height: 100px;
  border-radius: 4px;
  background-color: #409EFF;
  text-align: center;
  color: #fff;
  padding: 40px 20px;
  box-sizing: border-box;
  margin-right: 20px;
}
</style>
