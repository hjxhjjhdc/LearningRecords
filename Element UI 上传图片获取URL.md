# Element UI 上传图片获取URL

```
URL.createObjectURL(file.raw)
```

## eg:

```
handleAvatarSuccess(res, file) {
  this.imageUrl = URL.createObjectURL(file.raw);
  this.dialogImageUrl=res.msg
},
```

