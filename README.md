### introduction
Fasthttpapi is a lightweight and high-performance HTTP service component in the dotnet core platform that supports WebSocket and SSL！
Performance higher than ap.net web api 200%

**[Document](https://ikende.github.io/FastHttpApi/)**.

**[Samples](https://github.com/IKende/FastHttpApi/tree/master/samples)**

## Online case
[https://www.ikende.com](https://www.ikende.com)

## PerformanceTest
**[master/PerformanceTest](https://github.com/IKende/FastHttpApi/tree/master/PerformanceTest/Beetlex_VS_AspCore_webapi)**

![](https://i.imgur.com/BMj7b4a.png)

## Cluster configuration
### [Cluster configuration project](https://github.com/IKende/ClusterConfiguration)

## using
### Install Packet

```
Install-Package BeetleX.FastHttpApi
```
### Setting Server GC
`<ServerGarbageCollection>true</ServerGarbageCollection>`

### sample code
``` csharp
    [Controller]
    class Program
    {
        private static BeetleX.FastHttpApi.HttpApiServer mApiServer;
        static void Main(string[] args)
        {
            mApiServer = new BeetleX.FastHttpApi.HttpApiServer();
            mApiServer.Debug();
            mApiServer.Register(typeof(Program).Assembly);
            mApiServer.Open();
            Console.Write(mApiServer.BaseServer);
            Console.Read();
        }
        // Get /hello?name=henry 
        // or
        // Get /hello/henry
        [Get("{name}")]
        public object Hello(string name)
        {
            return $"hello {name} {DateTime.Now}";
        }
        // Get /GetTime  
        public object GetTime()
        {
            return DateTime.Now;
        }
        // Post /PostStream
        // name=aaa&value=bbb
        [Post]
        [NoDataConvert]
        public object PostStream(IHttpContext context)
        {
            Console.WriteLine(context.Data);
            string value = context.Request.Stream.ReadString(context.Request.Length);
            return value;
        }
        // Post /Post
        // {"name":"henry","value":"bbbb"}
        [Post]
        public object Post(string name, string value, IHttpContext context)
        {
            Console.WriteLine(context.Data);
            return $"{name}={value}";
        }
        
        // Post /PostForm
        // name=aaa&value=bbb
        [Post]
        [FormUrlDataConvert]
        public object PostForm(string name, string value, IHttpContext context)
        {
            Console.WriteLine(context.Data);
            return $"{name}={value}";
        }
    }
```
[samples](https://github.com/IKende/FastHttpApi/tree/master/samples)

## monitoring and management Services
#### Install Packet
```
Install-Package BeetleX.FastHttpApi.Admin -Version 0.6.2
```
#### Registering  management controller
```
mApiServer.Register(typeof(BeetleX.FastHttpApi.Admin._Admin).Assembly);
```
### access url
```
/_admin/index.html
```
![](https://i.imgur.com/mKrbW43.png)

![](https://i.imgur.com/K7zVzMx.png)

![](https://i.imgur.com/ASTgD2r.png)

![](https://i.imgur.com/q5mf7ee.png)
