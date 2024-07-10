---
{"dg-publish":true,"permalink":"/二维码批量生成器/","tags":["二维码","批量处理","效率方法"],"noteIcon":""}
---


想要个二维码生成器用作生成人升这款游戏化待办软件的打卡点，这类工具都需要会员才能进行那种很长的批量化处理。搞得我很生气，我就直接搞了个前端来实现：从Excel导入直接批量生成二维码，然后再打包下载。


```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Excel 批量生成二维码</title>

    <script src="https://cdn.jsdelivr.net/npm/xlsx/dist/xlsx.full.min.js"></script>

    <script src="https://cdn.jsdelivr.net/gh/davidshimjs/qrcodejs/qrcode.min.js"></script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.7.1/jszip.min.js"></script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>

</head>

<body>

  

<input type="file" id="upload" accept=".xlsx, .xls" />

<button onclick="generateQRFromExcel()">从 Excel 导入并生成二维码</button>

<button onclick="downloadAllQRs()">下载所有二维码</button>

<div id="qrcode-container"></div>

  

<script>

    // 从 Excel 导入并生成二维码

    function generateQRFromExcel() {

      var file = document.getElementById('upload').files[0];

      var reader = new FileReader();

      reader.onload = function(e) {

        var data = e.target.result;

        var workbook = XLSX.read(data, {

          type: 'binary'

        });

        workbook.SheetNames.forEach(function(sheetName) {

          var XL_row_object = XLSX.utils.sheet_to_row_object_array(workbook.Sheets[sheetName]);

          var qrcodeContainer = document.getElementById('qrcode-container');

          qrcodeContainer.innerHTML = ""; // 清空之前的二维码

          // 对每行数据生成二维码及文本标注

          XL_row_object.forEach(function(row) {

            var text = row[Object.keys(row)[0]];

            if (text) {

              var qrWrapDiv = document.createElement("div");

              var qrDiv = document.createElement("div");

              var textDiv = document.createElement("div"); // 用于文本标注

              textDiv.textContent = text.toString();

              qrWrapDiv.appendChild(qrDiv);

              qrWrapDiv.appendChild(textDiv);

              // 设置 div 属性以便下载时使用

              qrWrapDiv.setAttribute('data-text', text.toString());

              new QRCode(qrDiv, {

                text: text.toString(),

                width: 128,

                height: 128

              });

              qrcodeContainer.appendChild(qrWrapDiv); // 添加div到容器中

            }

          });

        });

      };

      reader.onerror = function(ex) {

        console.log(ex);

      };

      reader.readAsBinaryString(file);

    }

    // 下载所有二维码

    function downloadAllQRs() {

      var zip = new JSZip();

      var qrcodeContainer = document.getElementById('qrcode-container');

      var qrcodes = qrcodeContainer.querySelectorAll('div[data-text]');

      var count = 0;

      qrcodes.forEach(function(wrapDiv) {

        var canvas = wrapDiv.querySelector('canvas');

        var text = wrapDiv.getAttribute('data-text');

        // 将 canvas 转换为图片并添加到 zip 文件中

        canvas.toBlob(function(blob) {

            count++;

            zip.file(text + ".png", blob);

            // 当所有文件都添加到 zip 时，创建 zip 并提供下载

            if (count === qrcodes.length) {

              zip.generateAsync({type: "blob"}).then(function(content) {

                saveAs(content, "qrcodes.zip");

              });

            }

        });

      });

    }

    // 页面加载完毕后绑定下载按钮的点击事件

    document.addEventListener('DOMContentLoaded', function() {

      var downloadButton = document.getElementById('download');

      downloadButton.addEventListener('click', downloadAllQRs);

    });

    </script>

</body>

</html>
```


### 最开始的单个二维码生成
```html
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>二维码生成器</title>

<script src="https://cdn.jsdelivr.net/gh/davidshimjs/qrcodejs/qrcode.min.js"></script>

</head>

<body>

  

<div id="qrcode"></div>

  

<input type="text" id="text" placeholder="输入文本生成二维码">

<button onclick="generateQRCode()">生成二维码</button>

  

<script>

  function generateQRCode() {

    var text = document.getElementById("text").value;

    if(text.trim() === "") {

      alert("请输入文本！");

      return;

    }

  

    // 清空之前的二维码

    var qrcodeContainer = document.getElementById('qrcode');

    qrcodeContainer.innerHTML = "";

  

    // 生成新的二维码

    new QRCode(qrcodeContainer, {

      text: text,

      width: 128,

      height: 128

    });

  }

</script>

  

</body>

</html>
```