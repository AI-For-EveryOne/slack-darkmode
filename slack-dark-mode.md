## 1. asar コマンドをインストール

```
npm install -g asar

```

## 2. Slack.app から app.asar , app.asar.unpacked をコピー


```
mkdir -p ~/tmp/slack
cp /Applications/Slack.app/Contents/Resources/app.asar ~/tmp/slack
cp -r /Applications/Slack.app/Contents/Resources/app.asar.unpacked ~/tmp/slack

```

## 3. asar を展開

```
cd ~/tmp/slack
asar extract app.asar app
```

## 4. ssb-interop.bundle.js の先頭に追記

```
vim app/dist/ssb-interop.bundle.js
```

```javascript
document.addEventListener('DOMContentLoaded', function() {    
  fetch('https://raw.githubusercontent.com/AI-For-EveryOne/slack-darkmode/master/darkmode.css')    
  .then(function(response) {
    return response.text();
  })
  .then(function(css) {
    const style = document.createElement('style'); 
    style.innerHTML = css;
    document.head.appendChild(style);
  });
});
```


## 5. asar を作成

```
asar pack app app.asar
```


## 6. 作成したapp.asarをコピー

```
sudo cp app.asar /Applications/Slack.app/Contents/Resources
```

## 7. Slackを起動

```
open /Applications/Slack.app
```