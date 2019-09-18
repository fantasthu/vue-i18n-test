### vue-i18n-test

该项目用来测试自动国际化之后翻译工具的使用情况,基本模板是 vue-element-admin,测试文件夹路径./src/views/i18n-translate

#### 项目依赖库

- [vue-i18n](https://github.com/kazupon/vue-i18n)
- [vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/guide/advanced/i18n.html)
- [vue-i18n-generator](https://gitee.com/thesadboy/vue-i18n-generator)
- [vue-i18n-generator-translate](https://www.npmjs.com/package/vue-i18n-generator-translate)

#### 注意事项

1. 项目使用了 element,需要一起进行国际化
2. 用户的 language 选择设置在 cookie 中(也能够通过数据库建立 userSetting 表存储,跨机器设备)
3. 生成的文件本地做备份并不推送,需要在.gitignore 中添加 /translate
4. 翻译目录尽量使用./src/views
5. 无法引入 vue 使用 vue 实例的尽量不要出现中文,如果要用请移动到 views 文件外,保持 views 里都是视图文件(如果 vue-element-admin 存在这样的文件也一并移出去)

### 项目结构

1. 整体结构(vue-element-admin 默认目录)
   ![vue-element-admin](https://github.com/easterCat/vue-i18n-test/blob/test/src/assets/01.png?raw=true)

2. lang 目录结构
   ![lang](https://github.com/easterCat/vue-i18n-test/blob/test/src/assets/02.png?raw=true)

可以看出当前项目是没有 tw 的相关翻译,需要在./src/utils/lang 下新建 tw.js,并且在./src/utils/lang/index.js 下加入代码

```
......
import elementTwLocale from "element-ui/lib/locale/lang/zh-TW"; // element-ui lang
import twLocale from "./tw";
......

const messages = {
  ......
  tw: {
    ...twLocale,
    ...elementTwLocale
  }
};

```

将多余的路由进行隐藏

#### 进行抽离翻译

vue-i18n-generator 是一个抽离工具,`18n generate ./src/views`能够将当前文件夹所有中文抽离出来放到根目录一个文件中 ./zh_cn.js

> 使用的时候最好做下翻译的文件备份,该工具的 revert 命令不是很好使用,复原有概率失败

```
module.exports = {
	"i18n_translate_index_82": "简体中文",
	"i18n_translate_index_83": "繁体中文",
	"i18n_translate_index_84": "美式英文",
	"i18n_translate_index_85": "确认",
	"i18n_translate_index_86": "取消",
	"i18n_translate_index_87": "提交",
	"i18n_translate_index_88": "审核",
	"i18n_translate_index_89": "查询",
	"i18n_translate_index_90": "核对",
	"i18n_translate_index_91": "刘德华",
	"i18n_translate_index_92": "香港",
	"i18n_translate_index_93": "周杰伦",
	"i18n_translate_index_94": "台湾",
	"i18n_translate_index_95": "郭富城",
	"i18n_translate_index_96": "黎明",
	"i18n_translate_index_97": "大陆",
    ......
}
```

文件有路径作为 key 值,抽离的中文作为 value 的一个对象.但是只是抽离中文并不能满足我们的需求,毕竟不能使用一个文本一个文本的翻译的方式进行工作,所以在抽离后使用 vue-i18n-generator-translate 进行自动化翻译,该工具包含了 vue-i18n-generator 的抽离工作.

```
 i18ntranslate generate ./src/views/i18n-translate
```

现在可以看到生成了一个 translate 文件夹,里面是生成文件的备份,其中./translate/cache/tw/zh_TW.JS 是繁体的翻译,./translate/cache/zh/zh_CN.JS 是中文格式,./translate/cache/en/en.JS 是英文的翻译

./translate/cache/tw/zh_TW.JS

```
default: {
    ......
    "index_3":"繁體中文",
    "index_4":"美式英文",
    "index_5":"一些提醒的信息",
    ......
},
```

./translate/cache/en/en.JS

```
default: {
    ......
    "index_3":"traditional Chinese",
    "index_4":"American English",
    "index_5":"Some reminder information",
    ......
},
```

将对应翻译文件复制粘贴到./src/utils/lang 下对应的语言文件

![03](https://github.com/easterCat/vue-i18n-test/blob/test/src/assets/03.png?raw=true)
![04](https://github.com/easterCat/vue-i18n-test/blob/test/src/assets/04.png?raw=true)
![05](https://github.com/easterCat/vue-i18n-test/blob/test/src/assets/05.png?raw=true)

翻译完毕

#### 如何翻译

使用 opencc 进行中文译繁体,puppeteer 调用简易 chrome 进行自动翻译(也可以使用 translate.js 来调用 youdao/google/baidu 翻译来调用 api 翻译,速度能快 10 倍以上,但我的 ip 被封完了,只能找个稳点方法)
