<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 源码地址 https://github.com/yizhiamumu/xiaoshu
* 大家好，我是一只阿木木。
* 我爱小姝！
* 
*/

/* 首先，我们给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 90vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 接下来，准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始 */
`, `
/* 好像差点什么
 * 这是 Markdown 格式的，我需要变成更友好的格式
 * 简单，将Markdown格式翻译成HTML
 * 再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`, `/* 写封感谢信。
 * 感谢大家对我的关注。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `一只阿木木
====

坐标：杭州
程序员


我爱小姝
====


爱的宣言
----

* 关关雎鸠，在河之洲。
* 窈窕淑女，君子好逑。

爱的信念
----

. 那一刻，我升起风马，不为乞福，只为守候你的到来；
. 那一天，闭目在经殿香雾中，蓦然听见，你颂经中的真言；
. 那一月，我摇动所有的经桶，不为超度，只为触摸你的指尖；
. 那一年，磕长头匍匐在山路，不为觐见，只为贴着你的温暖；
. 那一世，转山转水转佛塔啊，不为修来生，只为途中与你相见。


爱的纪念
----

. 人生若只如初见，何事秋风悲画扇。
. 等闲变却故人心，却道故人心易变。 
. 骊山语罢清宵半，泪雨零铃终不怨。
. 何如薄幸锦衣郎，比翼连枝当日愿。


藏头诗
----

. 我来少年意如何，
. 爱此江湖一钓蓑。
. 小艇轻舟归去晚，
. 姝丽楼阁倚烟萝。


爱的誓言
----

. 在天愿作比翼鸟 在地愿为连理枝

博客关注
----

* [GitHub](https://github.com/yizhiamumu)
* [博客](www.cnblogs.com/yizhiamumu)
* [公众号]：一只阿木木

勾引方式
----
* 微信：yizhiamumu
* 电话:18668075001

我喜欢你是寂静的
----

* 我喜欢你是寂静的，彷佛你消失了一样\n*你从远处聆听我，我的声音却无法触及你。
* 好像你的双眼已经飞离去，如同一个吻，封缄了你的嘴。如同所有的事物充满了我的灵魂。你像我的灵魂，一只梦的蝴蝶。
* 我喜欢你是寂静的，好像你已远去。你听起来向在悲叹，一只如歌悲鸣的蝴蝶。你从远处听见我，我的声音无法企及你： 
* 让我在你的沉默中安静无声，并且让我藉你的沉默与你说话。你的沉默明亮如灯，简单如指环。你就像黑夜，拥有寂寞与群星。

* （by：一只阿木木）

  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) {
              return
            }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>
