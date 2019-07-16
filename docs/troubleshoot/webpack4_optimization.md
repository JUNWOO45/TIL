## webpack4 optimization

- Webpack4에서 CommonsChunkPlugin을 사용해보려고하는데..

  ```
  Error: webpack.optimize.CommonsChunkPlugin has been removed, please use config.optimization.splitChunks instead.
  ```

  이런 에러가 뜨네요.

  찾아보니, 웹팩4에서는 최적화 관련 플러그인이 모두 **optimization**으로 통합되었다고 합니다.

  ComonsChunkPlugin도 splitChunks로 바뀌었다네요!

  원래는..

  ```
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor' // Specify the common bundle's name.
    }),
  ]
  ```

  이런 식으로 사용하려고했는데 아예 바뀌었습니다.

  ```
  optimization: {
      splitChunks: {
        cacheGroups: {
          vendor: {
            chunks: 'initial',
            name: 'vendor',
            enforce: true,
          },
        },
      }
    }
  ```

  이렇게 사용했습니다.

  

  - 지금 name : 'vendor'인데... 'vendor11'로 바꾸면 dist폴더에 main.js, vendor.js, vendor11.js가 생성되어버리고 moment와 lodash는 vendor11.js에 들어가있네요. 

    이름 맞춰주는거 중요할듯.....

  

- 참고로, 최적화관련 플러그인이 모두 optimization으로 통합되었다고 했으니, splitChunk뿐 아니라 기존 UglifyJsPlugin도 minimize로 바뀌었다고 하네요.

  ```
  {
    optimization: {
      minimize: true/false,
      splitChunks: {},
      concatenateModules: true,
    }
  }
  ```

  구글링하며 찾아보니 이런 식으로 사용하나 봅니다!

  