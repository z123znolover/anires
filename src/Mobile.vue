<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*

* 大家好，我是张小童。
* 我来写一份简历！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .2s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54);
}
/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  overflow: auto;
  width: 90vw;
  margin: 2.5vh 5vw;
  height: 90vh;
}
/* 太高了 */
.styleEditor {
  height: 45vh;
}
/* 代码高亮 */
.token.selector{
  color: rgb(133,153,0);
}
.token.property{
  color: rgb(187,137,0);
}
.token.punctuation{
  color: yellow;
}
.token.function{
  color: rgb(42,161,152);
}

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  transform: rotateX(-10deg) translateZ(-50px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed;
  top: 50%; left: 0;
  padding: .5em;  margin: 2.5vh;
  width: 95vw; height: 45vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 开始写简历 */


`,
          `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
`, `
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
`],
        currentMarkdown: '',
        fullMarkdown: `张小童
====
坐标：湖南长沙。

java软件工程师，产品经理，项目经理。现为自由职业。

技能
====

数据库设计
----

  - noSQL设计

后端开发
----
  - 用户管理
  - 单点登录
  - 第三方登录
  - 权限管理
  - 交易系统
  - 支付系统
  - 社区系统
  - 博客系统
  - 公众号开发
  - 小程序开发
  - API接口

前端开发
----
  - Web前端开发
  

产品设计
----
  - 智慧旅游项目
  - 运动健康云平台
  - 社区支持农业O2O项目
  - 省级环境监控平台
  - 高速公路异地处罚系统
  - 环保局办公自动化系统
  - 保险公司数据迁移项目
  - 啤酒厂供应链项目
  - 货运代理系统
  - 集装箱管理系统
  - 滞期费管理项目

IT技能和语言能力
----
  - 熟悉Java编程，有良好的算法和编码能力，熟悉面向对象编程。
  - 熟悉JavaWeb, JDBC, 熟悉Http协议。
  - 熟悉Springmvc，Spring，MyBatis，了解Struts2, Hibernate等开源框架。
  - 熟悉应用服务器软件Tomcat等容器配置和部署，能够使用Linux操作系统。
  - 掌握JavaScript，Ajax，jQuery等前台开发技术。
  - 掌握MySql，熟练掌握sql语句。
  - 掌握分布式文件系统fastDFS原理、fastDFS的Java接口应用。
  - 掌握solr集群搭建及solrJ集群版的Java接口应用。
  - 掌握redis集群搭建及redis集群版Java接口的应用。
  - 了解集群下的并发解决方案，支持(HA)高可用(采用nginx,lvs)。
  - 会采用分布式缓存解决数据库压力。

工作经历
====

1. 湖南融耀健康管理有限公司
2. 太原网健科技有限公司
3. 合肥蓝盾科技有限公司
4. 上海易保网络有限公司
5. 厦门海环计算机软件有限公司

教育经历
====

1. 长春科技学院
2. 北京理工大学 java开发工程师

文章
====

* [故土难离（我的父亲母亲）](https://www.meipian.cn/qacqfbz?uuid=d541c15eef694065bc9d1ac9a07925a2)
* [油腻腻的中年（小诗）](https://www.meipian.cn/wjaz3zh?uuid=ca1cd053b717451da781786de44e66e7)
* [生命（老四们的蝼蚁人生）](https://www.meipian.cn/vc4pr59?uuid=799c98f5a187405c94c86f7da7788869)
* [大健康商业模式](http://www.sitexa.org/technology/%E5%A4%A7%E5%81%A5%E5%BA%B7%E5%95%86%E4%B8%9A%E6%A8%A1%E5%BC%8F.html)
* [社区社交商业模型](http://www.sitexa.org/other/%E7%A4%BE%E5%8C%BA%E7%A4%BE%E4%BA%A4%E5%95%86%E4%B8%9A%E6%A8%A1%E5%9E%8B.html)

链接
====

* [GitHub](https://github.com/z123znolover/resume)

勾引方式
====

* 微信：17610476521

自我介绍:
----

* 本人学识渊博、经验丰富，代码风骚、效率恐怖，前端、java无不精通，熟练掌握各种框架，深山苦练20余年，一天只睡4小时，千里之外定位问题，瞬息之间修复上线。
* 身体强壮、健步如飞，可连续编程100小时不休息，讨论技术方案5小时不喝水，上至带项目、出方案，下至盗账号、威胁pm，啥都能干。
* 泡面矿泉水已备好，学校不支持编程已辍学，家人不支持编程已断绝关系，老婆不支持编程已离婚，小孩不支持编程已送孤儿院，备用电源万兆光纤永不断电断网，门口已埋雷无人打扰

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          this.$nextTick(() => {
            this.$refs.resumeEditor.goTop()
          })
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
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
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    min-height: 100vh; position: relative;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }

</style>
