# subject-220624

### $.ajax ( jQuery ) : フォームを偽造するサーバへの送信
```javascript
    var formData = new FormData();

    $.ajax({
        url: "http://localhost/php-0623-01/ajax.php",
        type: "POST",
        data: formData,
        processData: false,  // jQuery がデータを処理しないよう指定
        contentType: false   // jQuery が contentType を設定しないよう指定
    })
    .done(function( data, textStatus ){
        console.log( "status:" + textStatus );
        console.log( "data:" + JSON.stringify(data, null, "    ") );

    })
    .fail(function(jqXHR, textStatus, errorThrown ){
        console.log( "status:" + textStatus );
        console.log( "errorThrown:" + errorThrown );
    })
    .always(function() {

    })
    ;
```

```php
header( "Content-Type: application/json; charset=utf-8" );
header( "Access-Control-Allow-Origin: *" );
```
