# webpack



webpack.common.js

```javascript
module: {
    rules: [
      {
        test: /\.(js|jsx|ts|tsx)$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        options: {
          presets: [
            [
              '@babel/preset-env',
              {
                targets: { browsers: ['> 0.2% in KR, not dead'] },
                debug: true,
                useBuiltIns: 'usage',
                corejs: 3,
              },
            ],
            ['@babel/preset-react', { runtime: 'automatic' }],
            '@babel/preset-typescript',
          ],
          plugins: [
            'babel-plugin-styled-components',
            isDevelopment && require.resolve('react-refresh/babel'),
          ].filter(Boolean),
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
        // exclude: /node_modules/,
      },
      {
        test: /\.svg$/,
        use: ['@svgr/webpack'],
      },
      {
        test: /\.(jpe?g|gif|png|webp|bmp|ttf|woff|otf|woff2)$/,
        type: 'asset/resource',
      },
    ],
  },
```



test에서 끝에 해당하는 확장자를 가진 애들을 다 뭘로 처리해주겠다 이런.
