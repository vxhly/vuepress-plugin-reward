# vuepress-plugin-reward

> A vuepress plugin for reward component

[![npm](https://img.shields.io/npm/v/vuepress-plugin-reward.svg)](https://www.npmjs.com/package/vuepress-plugin-reward)
[![GitHub stars](https://img.shields.io/github/stars/vxhly/vuepress-plugin-reward)](https://github.com/vxhly/vuepress-plugin-reward/stargazers)
[![GitHub license](https://img.shields.io/github/license/vxhly/vuepress-plugin-reward)](https://github.com/vxhly/vuepress-plugin-reward/blob/master/LICENSE)

## Install

``` bash
# install dependencies
npm i vuepress-plugin-reward -D

# or use yarn
yarn add vuepress-plugin-reward -D
```

## Show it like

![vuepress-reward](http://oss-blog.test.upcdn.net/vuepress-reward-1.png)

![vuepress-reward](http://oss-blog.test.upcdn.net/vuepress-reward-2.png)

## Coloring scheme

### The Button

`$accentColor` is taken from the configuration in `.vuepress/styles/palette.styl`

``` stylus
.demo {
  color: $accentColor;
  background-color: lighten($accentColor, 50%);
}
```

### The Reward Container

`$accentColor` and `$textColor` is taken from the configuration in `.vuepress/styles/palette.styl`

``` stylus
.demo {
  color: $accentColor; // First reward text and closed icon color.
  color: $textColor; // Second reward text and container body text color.
  border-color: lighten($textColor, 30%);
  background-color: #fff;
}
```

## Usage

Write vuepress config

``` javascript
module.exports = {
  plugins: ['reward']
}
```

## Options

This plugin supports the following configurations.

``` javascript
module.exports = {
  plugins: ['reward', {
    btnText: '打赏', // reward button text.
    title: '给作者赏一杯咖啡吧', // First reward text.
    subTitle: '您的支持将是我继续更新下去的动力', // Second reward text.
    rewardOption: [ // your QR code image.
      {
        text: '微信',
        url: '/WeChat.png' // ddd your picture to docs/.vuepress/public
      },
      {
        text: '支付宝',
        url: '/Alipay.png' // ddd your picture to docs/.vuepress/public
      }
    ],
    showInMobile: false // whether to display on the mobile side, default: false.
  }]
}
```

## License

[MIT](https://github.com/vxhly/vuepress-plugin-reward/blob/master/LICENSE).