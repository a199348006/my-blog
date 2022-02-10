---
title: "使用Express架設檔案上傳/下載API"
date: 2022-02-09T15:40:07+08:00
draft: true
tags: ["javascript", "express", "multer"]
categories: ["undefined"]
description: "檔案上傳使用multer，下載使用res.download() in Express"
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 網路上已有了許多教學及流程可以參考，在實作過程中還算順利，所以這邊就只附上我個人的[參考文獻](#參考來源)，並提出些碰到的狀況。

套件版本

- express: ^4.17.1
- multer: ^1.4.4

## API

### Upload File

#### Upload-server

util/middleware.js

```javascript
const multer = require('multer')

const storage = multer.diskStorage({
  destination: 'D:/upload-files',
  filename: function (req, file, callback) {
    callback(null, file.originalname)
  }
})
const upload = multer({ storage: storage }).single('file')

exports.uploadFile = (req, res, next) => {
  upload(req, res, function (err) {
    if(err instanceof multer.MulterError) {
      console.log('Multer error: ', err)
      res.status(400)
    } else if(err) {
      console.log('Upload error: ', err)
      res.status(400)
    } else {
      next()
    }
  })
}
```

routes/index.js

```javascript
const { uploadFile } = require('../util/middleware')

router.post('/upload', uploadFile, (req, res) => {
  console.log(req.file)
  console.log(req.body)
  res.status(200)
})
```

#### Upload-client

html

```html
<head>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>  
</head>
<body>
  <input type="file" id="myfile">
  <button id="btn-post">Click</button>

  <script>
    $("#btn-post").click(function () {     
      let formData = new FormData()
      formData.append('title', 'This is title.')
      formData.append('file', $("#myfile").prop("files")[0])
      
      axios({
        url: 'http://localhost:port/upload',
        method: 'POST',
        data: formData
      })
    })
  </script>
</body>
```

#### Upload-result

result with file

```node
{
  fieldname: 'file',
  originalname: 'ppt.pptx',
  encoding: '7bit',
  mimetype: 'application/vnd.openxmlformats-officedocument.presentationml.presentation',
  destination: 'D:/upload-files',
  filename: 'ppt.pptx',
  path: 'D:\\upload-files\\ppt.pptx',
  size: 341753
}
[Object: null prototype] { title: 'This is title.' }
```

result without file

```node
undefined
[Object: null prototype] { title: 'This is title.', file: 'undefined' }
```

### Download File

#### Download-server

controller/downloadFile.js

```javascript
exports.downloadFile = (req, res) => {
  const fileName = req.params.name
  const directoryPath = 'D:/upload-files/'

  res.download(directoryPath + fileName, fileName, (err) => {
    if(err) {
      res.status(500).send({ message: 'download fail: ' + err })
    }
  })
}
```

routes/index.js

```javascript
const { downloadFile } = require('../controller/downloadFile')

router.get('/downloadFile/:name', downloadFile)
```

#### Download-client

html

```javascript
axios({
  url: `http://localhost:port/downloadFile/${fileName}`, 
  method: 'GET',
  responseType: 'blob',
}).then((response) => {
  const url = window.URL.createObjectURL(new Blob([response.data]));
  const link = document.createElement('a');
  link.href = url;
  link.setAttribute('download', fileName); 
  document.body.appendChild(link);
  link.click();
});
```

[How to download files using axios](https://stackoverflow.com/questions/41938718/how-to-download-files-using-axios/53230807)

## 參考來源

[Multer GitHub](https://github.com/expressjs/multer)

[Multer example](https://www.twilio.com/blog/handle-file-uploads-node-express)

[Express: res.download()](https://expressjs.com/zh-tw/api.html#res.download)
