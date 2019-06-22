# CSS Fonts

- [Google web fonts downloader](https://google-webfonts-helper.herokuapp.com/fonts/rubik?subsets=latin)
- [CSS packages](https://github.com/css-pkg)
- [Postcss importing from node-modules]()


postcss.config.js
```js
module.exports = (ctx) => ({
  map: { inline: false },
  plugins: {
    'autoprefixer': {},
    'postcss-import': { root: ctx.file.dirname },
    'postcss-url': {
      url: 'copy',
      useHash: true,
      assetsPath: 'assets'
    },
    'postcss-browser-reporter': {},
    'postcss-reporter': {}
  }
})
```
