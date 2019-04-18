# Custom React Scripts

## 1/ Fork

## 2/ Custom

`package.json`  
```
  "dependencies": {
    [...]
    "graphql-tag": "2.10.1",
    "worker-loader": "2.0.0",
    "sharedworker-loader": "2.1.1"
  },
```

`config/webpack.config.js`  

prevent `window` ref error
```
output: {
  globalObject: 'this',
```

prevent build error
```
optimization: {
  noEmitOnErrors: false,
```

loaders
```
  [...]
  {
    // "oneOf" will traverse all following loaders until one will
    // match the requirements. When no loader matches it will fall
    // back to the "file" loader at the end of the loader list.
    oneOf: [
      {
        test: /\.worker\.js$/,
        include: path.appSrc,
        loader: require.resolve('worker-loader')
      },
      {
        test: /\.sharedworker\.js$/,
        include: path.appSrc,
        loader: require.resolve('sharedworker-loader')
      },
      {
        test: /\.(graphql|gql)$/,
        include: path.appSrc,
        loader: require.resolve('graphql-tag/loader'),
      },
```

## 3/ Pack

```
npm pack
```

may need to update the tgz file name

## 4/ create react app

```
npx create-react-app APP_NAME --scripts-version ../REACT_SCRIPTS_FOLDER/react-scripts-VERSION.tgz

npx create-react-app gitscout --scripts-version ../react-scripts-gs/react-scripts-2.1.8.tgz
```
