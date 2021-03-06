# 开发常见问题




## Q：如何关闭富文本XSS

系统默认启用了全站XSS过滤，如果您只是用CMS作为官网等后台产生富文本数据并且发现 HTML 样式丢失，可以选择关闭XSS过滤。

> **安全提示**：XSS是用户端常见的漏洞，非必要情况下强烈建议打开XSS过滤。

编辑文件 `vendor/modstart/modstart/src/Core/Util/HtmlUtil.php`

修改 `filter` 函数。

```php
class HtmlUtil{
    // ...
    public static function filter($content)
    {
        if (empty($content)) {
            return $content;
        }
        return Purifier::cleanHtml($content);
    }
    // ...
}
```

修改为

```php
class HtmlUtil{
    // ...
    public static function filter($content)
    {
        return $content;
    }
    // ...
}
```

## Q：系统是前后端分离的吗？

为提高开发效率，系统使用的是融合开发，不限制前端使用技术栈。

- 部分交互复杂的页面（如文档管理、CRM、模块管理、题库管理、数据导入等）使用的是前后端分离（ vue + 接口）
- 使用 Grid、Form、Detail 等内置组件快速开发的是 HTML + PHP 融合开发
