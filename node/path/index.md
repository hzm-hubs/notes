### 

### path.join()

语法：<code>path.join([...paths])</code>
* ...paths: <string> 路径片段的序列
* 返回：<string>
  
path.join() 方法使用特定于平台的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Returns: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// Throws 'TypeError: Path must be a string. Received {}' 
```

### path.resolve()
语法：<code>path.resolve([...paths])</code>
* ...paths: <string> 路径或路径片段的序列
* 返回：<string>

path.resolve() 方法将路径或路径片段的序列解析为绝对路径。给定的路径序列从右到左处理，每个后续的 path 会被追加到前面，直到构建绝对路径。例如，给定路径段的顺序：/foo、/bar、baz，调用 path.resolve('/foo', '/bar', 'baz') 将返回 /bar/baz，因为 'baz' 不是绝对路径，但 '/bar' + '/' + 'baz' 是。如果在处理完所有给定的 path 片段之后，还没有生成绝对路径，则使用当前工作目录。生成的路径被规范化，并删除尾部斜杠（除非路径解析为根目录）。零长度的 path 片段被忽略。如果没有传入 path 片段，则 path.resolve() 将返回当前工作目录的绝对路径。

```js
path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif' 
```
与join方法相比：

1、join是把各个path片段连接在一起， resolve把‘／’当成根目录
```js
path.join('/a', '/b'); 
// /a/b
path.resolve('/a', '/b');
// /b
```
2、resolve在传入非/路径时，会自动加上当前目录形成一个绝对路径，而join仅仅用于路径拼接
```js
// 当前路径为
/Users/xiao/work/test
path.join('a', 'b', '..', 'd');
// a/d
path.resolve('a', 'b', '..', 'd');
// /Users/xiao/work/test/a/d
```
3、当二者已<code>__dirname</code>开始，俩者结果一致
```js
console.log(path.resolve(__dirname, , "assets.less"));
//输出： /Users/Documents/Code/vite-app/assets.less                                                     
console.log(path.join(__dirname, "assets.less"));
//输出： /Users/Documents/Code/vite-app/assets.less                                                     
```

### path.dirname(path)
* ...paths: <string> 
* 返回：<string>
path.dirname() 方法返回 path 的目录名
```js
path.dirname('/foo/bar/baz/asdf/quux');
// Returns: '/foo/bar/baz/asdf' 
```