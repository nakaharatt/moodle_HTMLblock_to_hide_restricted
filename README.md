# Moodle Tips
# 利用制限のテキストを表示/非表示するためのHTMLブロック

利用制限の表示を切り替えたいコースにHTMLブロックを作成し以下のソースを貼り付けて保存する。

コースアクセス時は非表示になる。

```
<button onclick='custom_hiderestricted();' class='btn btn-primary hiderestrictedbtn' hidestatus='0'>利用制限を隠す</button>
<script>
function custom_hiderestricted(action){
    var btn = document.getElementsByClassName('hiderestrictedbtn');
    if(btn[0].getAttribute('hidestatus') == 0 || action == 'hide'){
        for( var i = 0; i < btn.length; i++  ){
            btn[i].setAttribute('hidestatus','1');
            btn[i].innerHTML = '<span lang="ja" class="multilang">利用制限を表示</span><span lang="en" class="multilang">Show restricted</span>';
            btn[i].classList.remove('btn-primary');
            btn[i].classList.add('btn-info');
            btn[i].setAttribute('hidestatus',1);
        }

        var restrictedelements = document.getElementsByClassName('availabilityinfo isrestricted');
        for( var i = 0; i < restrictedelements.length; i++  ){
            restrictedelements[i].setAttribute('style','display:none');
        }
    }else{
        for( var i = 0; i < btn.length; i++  ){
            btn[i].setAttribute('hidestatus','0');
            btn[i].innerHTML = '<span lang="ja" class="multilang">利用制限を隠す</span><span lang="en" class="multilang">Hide restricted</span>';
            btn[i].classList.remove('btn-info');
            btn[i].classList.add('btn-primary');
            btn[i].setAttribute('hidestatus',0);
        }

        var restrictedelements = document.getElementsByClassName('availabilityinfo isrestricted');
        for( var i = 0; i < restrictedelements.length; i++  ){
            restrictedelements[i].removeAttribute('style');
        }
    }
}

window.onload = function(){
    custom_hiderestricted('hide');
}
</script>
```


:warning:多言語フィルタがONになっているものとしてボタンの文字列を設定しているので、OFFの場合は適宜書き換えること。

2021/09/08 Moodle3.9とMoodle3.11で動作検証
