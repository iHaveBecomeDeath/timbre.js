T("interval")
=============
{timer} Interval

## Description ##

指定した間隔で入力オブジェクトに対して `bang()` します。

`delay` の設定が無い場合は `start()` の後、
JavaScript の setInterval と同じように `interval` と同じ時間の待機ののち動作を開始します。

```timbre
var freqs = T([220, 440, 660, 880]);

var osc = T("sin", {freq:freqs, mul:0.5});
var env = T("perc", {a:50, r:500}, osc).bang();

var i = T("param", {value:500}).linTo(50, "30sec");

T("interval", {interval:i}, freqs, env).start();

env.play();
```

## Properties ##
- `interval` _(T Object or timevalue)_
  - 入力オブジェクトに対して `bang()` を呼び出す間隔を設定します
- `delay` _(Number or timevalue)_
  - 待機時間を設定します
- `count` _(Number)_
  - `bang` を送出した回数
- `timeout` _(Number or timevalue)_
  - タイムアウトの時間を設定します
- `currentTime` _(Number)_
  - 経過時間

## Methods ##
- `bang()`
  - 動作を再開します。

## Events ##
- `ended`
  - タイムアウト時に発生します。
  
## Note ##
オブジェクト生成時に `once` を設定すると Deferred オブジェクトとなり、各Deferredメソッドのサポートとタイムアウト時に resolve、タイムアウト前に停止した場合に reject されます。

```timbre
T("interval", {timeout:2500, once:true}, function(count) {
    console.log(count);
}).then(function() {
    this.pause();
}).start();
```

## See Also ##
- [T("timeout")](./timeout.html)

## Source ##
https://github.com/mohayonao/timbre.js/blob/master/src/objects/interval.js