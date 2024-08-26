# Шпаргалки по JS

## JQuery get-запрос

```Javascript
function get(url) {
    return $.ajax({
        type: "GET",
        url: url,
        async: false
    }).responseText;
}
```

## Параметры из URL

```Javascript
const params = new URLSearchParams(window.location.search);
params.has('test');
params.get('test');

for (const param of params) {
  console.log(param)
}
```

## DragAndDrop File Zone (JQuery)

```Javascript
dropFileZone.on('drag dragstart dragend dragover dragenter dragleave drop', function(e) {
    e.preventDefault();
    e.stopPropagation();
})
    .on('dragover dragenter', function() {
        dropFileZone.addClass('dragover');
    })
    .on('dragleave dragend drop', function() {
        dropFileZone.removeClass('dragover');
    })
    .on('drop', function(e) {
        let index;
        let filesList = e.originalEvent.dataTransfer.files;
        for (index = 0; index < filesList.length; ++index) {
            createPhotoAfterUpload(filesList[index]);
        }
    });
```

## Открыть ссылку в новой вкладке

```Javascript
function openInNewTab(href) {
  Object.assign(document.createElement('a'), {
    target: '_blank',
    rel: 'noopener noreferrer',
    href: href,
  }).click();
}
```