# vuepress-plugin-meting <GitHubLink repo="moefyit/vuepress-plugin-meting"/>

:cake: A simple plugin connect APlayer, Meting and VuePress.

<p align="center">
   <a href="https://www.npmjs.com/package/vuepress-plugin-meting" target="_blank"><img alt="npm" src="https://img.shields.io/npm/v/vuepress-plugin-meting.svg"></a>
   <a href="https://github.com/moefyit/vuepress-plugin-meting/stargazers" target="_blank"><img alt="GitHub stars" src="https://img.shields.io/github/stars/moefyit/vuepress-plugin-meting"></a>
   <a href="https://www.npmjs.com/package/vuepress-plugin-meting" target="_blank"><img alt="downloads" src="https://img.shields.io/npm/dt/vuepress-plugin-meting.svg"></a>
   <a href="https://www.npmjs.com/package/vuepress-plugin-meting" target="_blank"><img alt="downloads" src="https://img.shields.io/npm/dm/vuepress-plugin-meting.svg"></a>
   <a href="https://github.com/moefyit/vuepress-plugin-meting/blob/master/LICENSE" target="_blank"><img alt="GitHub license" src="https://img.shields.io/github/license/moefyit/vuepress-plugin-meting"></a>
</p>

- Document: [meofy-vuepress](https://moefyit.github.io/meofy-vuepress/)
- LiveDemo: [www.sigure.xyz](https://www.sigure.xyz/)

<Meting server="netease"
        type="playlist"
        mid="2539599584"
        :lrc-type="3"/>

## Install

``` bash
yarn add vuepress-plugin-meting -D
# or use npm
npm i vuepress-plugin-meting -D
```

## Usage

``` javascript
module.exports = {
  plugins: [
    'meting', {
      metingApi,
      meting,
      aplayer
    }
  ]
}
```

使用该插件后将自动注册 `<Meting/>` 组件与 `<APlayer/>` 组件，你可以在任意位置使用它们

- `<Meting/>` 组件支持 `meting` Options 和 `aplayer` Options，其中 `aplayer` 的 `audio` 选项将自动通过 metingApi 获取
- `<APlayer/>` 组件支持 `aplayer` Options，当然，你需要自行提供 `audio` 音乐源

`config.js` 中的 `meting` 选项和 `aplayer` 选项是全局 UI 组件的配置项，当 `meting` 选项被配置后，将自动注册一个全局 UI 组件 `<Meting/>`（吸底模式），这两个配置项不影响其他组件的配置项

## Options

Options 分为 `metingApi`、`meting`、`aplayer` 三部分

### metingApi

即 `Meting` 的 `api`，默认为 @metowolf 提供的 `api`，你也可以通过自建修改该选项

### meting

`Meting` 相关选项

- server
   - 类型：`string`
   - 默认值： `undefined`
   - 描述：MetingApi 中的 `server` 参数，即音乐平台
   - 可选值： `"netease" | "tencent" | "xiami"`

- type
   - 类型：`string`
   - 默认值： `undefined`
   - 描述：MetingApi 中的 `type` 参数，即资源类型（播放列表、单曲、专辑等）
   - 可选值： `"song" | "album" | "artist" | "playlist"`

- mid
   - 类型：`string`
   - 默认值： `undefined`
   - 描述：MetingApi 中的 `id` 参数，即资源 ID

- auto
   - 类型：`string`
   - 默认值：`""`
   - 描述：资源 `url`，填写后可通过资源 `url` 自动解析资源平台、类型、ID，上述三个选项将被覆盖

该 Option 可分别填写 `server`、`type`、`mid`

``` javascript
meting: {
  server: "netease",
  type: "playlist",
  mid: "2539599584",
}
```

也可以只填写 `auto`

``` javascript
meting: {
  auto: "https://music.163.com/#/playlist?id=2539599584"
}
```

### aplayer

> 详情见 [vue-aplayer 文档](https://aplayer.moefe.org/docs/options/)

- fixed
   - 类型：`boolean`
   - 默认值： `false`
   - 描述：是否开启吸底模式

- mini
   - 类型：`boolean`
   - 默认值： `false`
   - 描述：是否开启迷你模式

- autoplay
   - 类型：`boolean`
   - 默认值： `false`
   - 描述：是否开启自动播放

- theme
   - 类型： `string`
   - 默认值： `#b7daff`
   - 描述：设置播放器默认主题颜色

- loop
   - 类型：`APlayer.LoopMode`
   - 默认值： `all`
   - 描述：设置播放器的初始循环模式
   - 可选值：`'all' | 'one' | 'none'`

- order
   - 类型：`APlayer.OrderMode`
   - 默认值： `list`
   - 描述：设置播放器的初始顺序模式
   - 可选值： `'list' | 'random'`

- preload
   - 类型：`APlayer.Preload`
   - 默认值： `auto`
   - 描述：设置音频的预加载模式
   - 可选值：`'none' | 'metadata' | 'auto'`

- volume
   - 类型：`number`
   - 默认值： `0.7`
   - 描述：设置播放器的音量

- audio（见 [vue-aplayer 文档](https://aplayer.moefe.org/docs/options/#audio)）

- customAudioType（见 [vue-aplayer 文档](https://aplayer.moefe.org/docs/options/#customaudiotype)）

- mutex
   - 类型：`boolean`
   - 默认值： `true`
   - 描述：是否开启互斥模式

- lrcType
   - 类型：`APlayer.LrcType?`
   - 默认值： `0`
   - 描述：设置 lrc 歌词解析模式
   - 可选值： `3 | 1 | 0`（`0`：禁用 lrc 歌词，`1`：lrc 格式的字符串，`3`：lrc 文件 url）

- listFolded
   - 类型：`boolean`
   - 默认值： `false`
   - 描述：是否折叠播放列表

- listMaxHeight
   - 类型：`number`
   - 默认值： `250`
   - 描述：设置播放列表最大高度，单位为像素

- storageName
   - 类型：`string`
   - 默认值： `vuepress-plugin-meting`
   - 描述：设置存储播放器设置的 `localStorage` key

## Examples

``` javascript
// .vuepress/config.js
module.exports = {
  plugins: [
    'meting', {
      metingApi: "https://meting.sigure.xyz/api/music",
      meting: {
        server: "netease",
        type: "playlist",
        mid: "2539599584",
      },          // 不配置该项的话不会出现全局播放器
      aplayer: {
        lrcType: 3
      }
    }
  ]
}
```

``` markdown
<!-- about.md -->

<Meting server="netease"
        type="playlist"
        mid="2539599584"
        :lrc-type="3"/>

<!-- 这样就可以在 about.html 页面单独引入一个播放器咯～ -->
```

## Thanks

- [APlayer](https://github.com/MoePlayer/APlayer)
-  [VueAPlayer](https://github.com/MoePlayer/vue-aplayer)
-  [Meting](https://github.com/metowolf/Meting)
-  [MetingJS](https://github.com/metowolf/MetingJS)
