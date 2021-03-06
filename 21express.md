## 中间件
basicAuth
body-parser
json
urlencoded
compress
cookie-parser
cookie-session
express-session
csurf
directory
errorhandler
static-favicon
morgan
method-override
query
response-time
static
vhost

## 邮件
### 1.概念
SMTP MSA MTA

### 2.插件
nodemailer

## 监控
[UptimeRobot](http://UptimeRobot.com)
[Pingdom](http://pingdom.com)
[Site24x7](http://www.site24x7.com/zhcn/index.html)





# 代码段

## 上传保存文件

```javascript

exports.saveFile = function(req, res, next) {
    var posterData = req.files.filefield
    var filePath = posterData.path
    var originalFilename = posterData.originalname
    if (originalFilename) {
        fs.readFile(filePath, function(err, data) {
            var jsVersion = req.body.jsVersion
            var type = posterData.extension
            var poster = jsVersion + '.' + type
            var newPath = path.join(__dirname, '../', '/hybrid-bundle-repository/bundle/' + poster)

            fs.writeFile(newPath, data, function(err) {
                req.poster = '/hybrid-bundle-repository/bundle/' + poster
                next()
            })
        })
    } else {
        next()
    }
};
```


## keystone 数据库操作
```javascript
var keystone = require('keystone'),
    Types = keystone.Field.Types;
 
var Post = new keystone.List('Post', {
    autokey: { path: 'slug', from: 'title', unique: true },
    map: { name: 'title' },
    defaultSort: '-createdAt',
    drilldown: 'author' // 在上面的例子中，author被定义为一个Relationship域
});
 
Post.add({
    title: { type: String, required: true },
    state: { type: Types.Select, options: 'draft, published, archived', default: 'draft' },
    author: { type: Types.Relationship, ref: 'User' },
    createdAt: { type: Date, default: Date.now },
    publishedAt: Date,
    image: { type: Types.CloudinaryImage },
    content: {
        brief: { type: Types.Html, wysiwyg: true, height: 150 },
        extended: { type: Types.Html, wysiwyg: true, height: 400 }
    }
});
 
Post.defaultColumns = 'title, state|20%, author, publishedAt|15%'

Post.schema.methods.isPublished = function() {
    return this.state == 'published';
}

Post.schema.pre('save', function(next) {
    if (this.isModified('state') && this.isPublished() && !this.publishedAt) {
        this.publishedAt = new Date();
    }
    next();
});


Post.register();
```

### 问题
- Keystone not start on node 7.x.

- Error: Module version mismatch, Expected 47, got 48

node的版本不对，sharp要求是6.10.0， 切换版本后rebuild ``` npm rebuild```

