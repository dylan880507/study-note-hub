

# 1>.net core中的Session以及HttpContext对象使用小结

## 1-1>https://www.jianshu.com/p/0315aa029867

*在MVC Controller里使用HttpContext.Session

```C#
HttpContext.Session.SetString("code","123456");
ViewBag.Code=HttpContext.Session.GetString("code");
```

*如果不是在Controller里，你可以注入IHttpContextAccessor，有两种方式，一种是在类的构造函数里面注入，如下：

```c#
public class SomeOtherClass
{
   private readonly IHttpContextAccessor _httpContextAccessor;
   private ISession _session=> _httpContextAccessor.HttpContext.Session;

   public SomeOtherClass(IHttpContextAccessor httpContextAccessor)
   {
      _httpContextAccessor=httpContextAccessor;      
   }

   public void Set()
   {
     _session.SetString("code","123456");
   }

   public void Get()
   {
     string code = _session.GetString("code");
   }
}
```

*另外一种是通过IServiceProvider，这时需要在startup中Configure中得到这个对象，然后通过

```c#
Microsoft.AspNetCore.Http.IHttpContextAccessor factory = app.ApplicationServices.GetService<Microsoft.AspNetCore.Http.IHttpContextAccessor>();
Microsoft.AspNetCore.Http.HttpContext context = factory.HttpContext;
```

或者

```c#
Microsoft.AspNetCore.Http.IHttpContextAccessor factory = app.ApplicationServices.GetService(typeof(Microsoft.AspNetCore.Http.IHttpContextAccessor));
Microsoft.AspNetCore.Http.HttpContext context = factory.HttpContext;
```

## 1-2>若出现Error unprotecting the session cookie.The payload was invalid，则参考下面文章，增加services.AddDataProtection()，然后重启浏览器。

https://www.cnblogs.com/vipsoft/p/13045581.html

## 1-3>若出现警告 No XML encryptor configured. Key may be persisted to storage in unencrypted form，则参考下面文章处理(没弄出来)

https://www.cnblogs.com/dudu/p/9589012.html
https://www.pianshen.com/article/14361061895

```powershell
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout dylan.key -out dylan.crt -subj "/CN=dylan.com" -days 3650
openssl pkcs12 -export -out dylan.pfx -inkey dylan.key -in dylan.crt -certfile dylan.crt -passout pass:
dylan.key
```



# 2>net core 注入log4net(可以在startup或者programme配置)

*注意：DatePattern中的value，如果使用.log，因为是关键字，则需要配置成'.log'

## 2-1>相关知识站点

https://www.cnblogs.com/kevin860/p/13170107.html
https://www.cnblogs.com/zxp6/p/12464559.html
https://blog.csdn.net/MrLsss/article/details/109258064
https://blog.csdn.net/liangmengbk/article/details/107729402

## 2-2>log4net.config配置

https://www.cnblogs.com/kevin860/p/13170107.html
https://www.cnblogs.com/changsen-wang/p/14275037.html

```C#
.ConfigureLogging((context, loggingBuilder) =>
{
	loggingBuilder.SetMinimumLevel(LogLevel.Warning);
	loggingBuilder.AddFilter("System", LogLevel.Information);
	loggingBuilder.AddFilter("Microsoft", LogLevel.Information);

/*第二种，在ConfigureLogging配置log4net begin*/
var cfgFilePath = Path.Combine(FramePublicFun.GetDllPath(), SysContant.Log4Net_CfgFileName);
loggingBuilder.AddLog4Net(cfgFilePath);
/*第二种，在ConfigureLogging配置log4net end*/

})
在Configure将日志对象注册到全局静态变量
//注册系统中静态类的框架日志服务
loggerFactory.RegisterGlobaltLogger();
```



## 2-3>内置日志记录提供程序

(1) 控制台
logging.AddConsole(); dotnet run 查看控制台日志记录输出。  
(2) 调试
logging.AddDebug(); 在 Linux 中，此提供程序将日志写入 /var/log/message。
(3) EventSource
logging.AddEventSourceLogger(); 在 Windows 中，它使用 PerfView 实用工具收集和查看日志，但尚无支持 Linux 或 macOS 的事件集合和显示工具。
(4) EventLog
logging.AddEventLog();向 Windows 事件日志发送日志输出。
(5) TraceSource
logging.AddTraceSource(sourceSwitchName);应用必须在 .NET Framework（而非 .NET Core）上运行。
2-4>appsettings.json中日志配置的解读, 可参考官网 https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/logging/?view=aspnetcore-5.0

```json
{
  "Logging": {
    "LogLevel": { // All providers, LogLevel applies to all the enabled providers.
      "Default": "Error", // Default logging, Error and higher.
      "Microsoft": "Warning" // All Microsoft* categories, Warning and higher.
    },
    "Debug": { // Debug provider.
      "LogLevel": {
        "Default": "Information", // Overrides preceding LogLevel:Default setting.
        "Microsoft.Hosting": "Trace" // Debug:Microsoft.Hosting category.
      }
    },
    "EventSource": { // EventSource provider
      "LogLevel": {
        "Default": "Warning" // All categories of EventSource provider.
      }
    }
  }
}
```



# 3>net core 部署 IIS

## 3-1>使用vs部署文件系统



## 3-2>直接到发布文件夹，执行dotnet **.dll --urls="http://\**:8099"，既可使用kestrel服务器



## 3-3>IIS部署方式

用IIS部署网站后, 看看网站里的"模块", 是否有AspNetCoreModuleV2, 若没有, 则需要下载net core运行时(根据net core版本下载对应的运行时版本)
https://www.cnblogs.com/zhangmm96/p/12102015.html
https://blog.csdn.net/weixin_33770878/article/details/94745175
https://www.cnblogs.com/MrHSR/p/10276650.html

*当发布后, 文件中有一个web.config. 在web.config中设置 ASPNETCORE_ENVIRONMENT 环境变量. 使用 web.config 设置 ASPNETCORE_ENVIRONMENT 环境变量后, 它的值会替代系统级设置.

```xml
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" arguments=".\ZhaoXiNetCoreDemo.dll" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" hostingModel="inprocess" >
		<environmentVariables>
			<environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
		</environmentVariables>
	  </aspNetCore>
    </system.webServer>
  </location>
</configuration>
```





# 4>ASP.Net Core解读launchSettings.json

https://www.cnblogs.com/qtiger/p/12958493.html
*通过配置ASPNETCORE_ENVIRONMENT来实现多环境切换, 系统内置3个环境名: Development（开发环境）, Staging（测试环境）, Production（生产环境）, 环境名也可以自定义.
如果发布项目未设置 ASPNETCORE_ENVIRONMENT，则默认为 Production. (本机vs中项目Properties\launchSettings.json中environmentVariables默认设置的是Development, 如果禁用environmentVariables, 那默认则为Production).
*多环境配置可参考官网
https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/environments?view=aspnetcore-3.1#environment-based-startup-class-and-methods
https://www.cnblogs.com/MrHSR/p/10276650.html
*在Startup里, Configure名字不是一定的, 如果环境是Development, 则Configure可以是ConfigureDevelopment, 如果没有ConfigureDevelopment, 也没有Configure, 则系统会报错.
*当 ASP.NET Core 应用启动时, 会启动Startup类. 应用程序可以为不同的环境, 单独定义 Startup 类. 可以定义例如: StartupDevelopment, StartupProduction, Startup.
当程序运行时会选择相应的 Startup 类. 程序会优先考虑名称后缀与当前环境相匹配的类. 如果是Developmen环境则程序进入StartupDevelopment, 如果是Production环境则程序进入StartupProduction.
如果找不到匹配的 Startup{EnvironmentName}, 就会使用 Startup 类.





# 5>ASP.NET Core中间件(Startup.Configure)

https://www.cnblogs.com/whuanle/p/10095209.html
https://www.cnblogs.com/stulzq/p/7760648.html
https://www.cnblogs.com/JNLightGade/p/5737485.html

## 5-1>常见中间件顺序

异常/错误处理
HTTP 严格传输安全协议
HTTPS 重定向
静态文件服务器
Cookie 策略实施
身份验证
会话
MVC

## 5-2>HTTP管道容器由三个扩展的方法来控制中间件的路由、挂载等等，分别是Run, Use, Map.

### 5-2-1>Run方法会使得可以使管道短路，顾名思义就是终结管道向下执行, 不会调用next()委托, 所以Run方法最好放在管道的最后来执行。

*处理Response.WriteAsync()中文乱码
https://blog.csdn.net/lovestj/article/details/98731058

### 5-2-2>Use不会主动短路整个HTTP管道，但是也不会主动调用下一个中间件，必须自行调用await next.Invoke(); 如果不使用这个方法去调用下一个中间件，那么Use此时的效果其实和Run是相同的。

UseWhen是Use的一个条件判断，当满足某个条件的时候，执行某个中间件。

### 5-2-3>Map可以根据提供的URL来路由中间件

MapWhen是Map的一个条件判断的扩展方法，可以通过它来判断某个条件适合的时候，执行某一个中间件(*通姑demo发现, usewhen和mapwhen的效果一样)

## 5-3>内置中间件

Authentication	提供身份验证支持
CORS	配置跨域资源共享
Response Caching	提供缓存响应支持
Response Compression	提供响应压缩支持
Routing	定义和约束请求路由
Session	提供用户会话管理
Static Files	为静态文件和目录浏览提供服务提供支持
URL Rewriting Middleware	用于重写 Url，并将请求重定向的支持

## 5-4>构建中间件的流程参考https://www.cnblogs.com/stulzq/p/7760648.html

```C#
public class MyMiddleware
{
    private readonly RequestDelegate _next;

	public MyMiddleware(RequestDelegate next)
	{
	    _next = next;
	}

	public async Task Invoke(HttpContext httpContext)
	{
	    await _next(httpContext);
	}
}

public static class MyMiddlewareExtensions
{
	public static IApplicationBuilder UseRequestCulture(
		this IApplicationBuilder builder)
	{
		return builder.UseMiddleware<MyMiddleware>();
	}
}
```

最后在Startup.Configure

```C#
app.UseRequestCulture();
```

## *5-5>因为中间件是在应用程序启动时构建的，而不是每个请求，所以在每个请求期间，中间件构造函数使用的作用域生命周期服务不会与其他依赖注入类型共享。 

如果您必须在中间件和其他类型之间共享作用域服务，请将这些服务添加到Invoke方法的签名中。 Invoke方法可以接受由依赖注入填充的其他参数。
例如上面的Invoke，改成如下

```C#
public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
{
	svc.MyProperty = 1000;
	await _next(httpContext);
}
```

或者

```C#
public class RequestLoggerMiddleware
{
	private readonly RequestDelegate _next;
	private readonly ILogger _logger;

public RequestLoggerMiddleware(RequestDelegate next, ILoggerFactory loggerFactory)
{
	_next = next;
	_logger = loggerFactory.CreateLogger<RequestLoggerMiddleware>();
}

public async Task Invoke(HttpContext context)
{
	_logger.LogInformation("Handling request: " + context.Request.Path);
	await _next.Invoke(context);
	_logger.LogInformation("Finished handling request.");
}

}
public static class RequestLoggerExtensions
{
    public static IApplicationBuilder UseRequestLogger(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<RequestLoggerMiddleware>();
    }
}
```

最后在Startup.Configure

```c#
app.UseRequestLogger();
```

## *5-6>若要在中间件内获取控制器名称和动作名等信息, 需要将自定义的中间件放在app.UseRouting()后, 可参考下面文章.

https://q.cnblogs.com/q/116803/

## *5-7>中间件的注册，还可以使用继承于IStartupFilter来实现，可参考https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/startup?view=aspnetcore-3.1





# 6>ASP.NET Core ConfigureServices

https://www.cnblogs.com/artech/p/dependency-injection-in-asp-net-core.html
https://www.cnblogs.com/dotNETCoreSG/p/aspnetcore-3_1-application-startup.html
https://blog.csdn.net/weixin_30604651/article/details/98671957

## 6-1>拓展知识

ASP.NET Core中的依赖注入（1）：控制反转（IoC）(https://www.cnblogs.com/artech/p/asp-net-core-di-ioc.html)
ASP.NET Core中的依赖注入（2）：依赖注入（DI）(https://www.cnblogs.com/artech/p/asp-net-core-di-di.html)
ASP.NET Core中的依赖注入（3）: 服务的注册与提供(https://www.cnblogs.com/artech/p/asp-net-core-di-register.html)
ASP.NET Core中的依赖注入（4）: 构造函数的选择与服务生命周期管理(https://www.cnblogs.com/artech/p/asp-net-core-di-life-time.html)
ASP.NET Core中的依赖注入（5）：ServicePrvider实现揭秘【总体设计】(http://www.cnblogs.com/artech/p/asp-net-core-di-service-provider-1.html)
ASP.NET Core中的依赖注入（5）：ServicePrvider实现揭秘【解读ServiceCallSite】(http://www.cnblogs.com/artech/p/asp-net-core-di-service-provider-2.html)
ASP.NET Core中的依赖注入（5）：ServicePrvider实现揭秘【补充漏掉的细节】(http://www.cnblogs.com/artech/p/asp-net-core-di-service-provider-3.html)

## 6-2>ConfigureServices允许返回一个ServiceProvider，这个特性的重要意义在于它使我们可以实现与第三方DI框架（比如Unity、Castle、Ninject和AutoFac等）的集成。

*3.X 引入autofac第三方依赖注入框架
https://www.cnblogs.com/oec2003/p/13069058.html
https://www.cnblogs.com/diwu0510/p/11562248.html
https://www.cnblogs.com/ingstyle/p/11836157.html
https://www.cnblogs.com/zxtceq/p/14156142.html

步骤：

### 6-2-1>引入Nuget包, Autofac, Autofac.Extensions.DependencyInjection, Autofac.Extras.DynamicProxy

### 6-2-2>修改Program.cs, 加入 .UseServiceProviderFactory(new AutofacServiceProviderFactory())

### 6-2-3>修改Startup, 添加方法 ConfigureContainer

```c#
public void ConfigureContainer(ContainerBuilder builder)
{
	//注册依赖注入模块
	builder.RegisterModule
	(
		new AutofacModuleRegister
		(
			FramePublicFun.GetDllPath(),
			new List<string>
			{
				"Dylan.FrameWork.dll"
			},
			true,
			typeof(Program)
		)
	);
}
```

### 6-2-4>配置Controller全部由Autofac创建(若不配置，则Controller的依赖注入由原本的框架实现)

在Startup.ConfigureServices中配置 services.AddControllersWithViews().AddControllersAsServices();
并在ConfigureContainer中添加如下代码，实现控制器的属性注入(也可以封装到批量注册的Load函数内)

```C#
var controllerBaseType = typeof(ControllerBase);
builder.RegisterAssemblyTypes(typeof(Program).Assembly)
    .Where(t => controllerBaseType.IsAssignableFrom(t) && t != controllerBaseType)
    .PropertiesAutowired();
```



### 6-2-5>在控制器中使用Autofac依赖注入

*可以在构造函数获取依赖注入的对象
*在Action可以通过[FromServices]参数，来获取依赖注入的对象
*可以使用属性注入，属性一定要为public

```C#
/// <summary>
/// 属性注入
/// </summary>
public ITestClass TestClassP
{
	get; set;
}
```



### 6-2-6>在其他类中使用依赖注入, 可是使用构造函数的依赖注入, 以及属性的依赖注入, 属性依赖注规则与控制器相同。

### 6-2-7>设置全局AutofacContainer

https://blog.csdn.net/sammy520/article/details/114417763

### 6-2-8>面向AOP，就是使用接口拦截, 拦截器注册要在使用拦截器的接口和类型之前, 在接口上添加拦截器，当调用接口的方法时，都会进入拦截器。

*控制器慎用AOP，容易报错，更建议用框架自带的filter特性

### 6-2-9>IServiceProvider和IComponentContext获取到的服务实例与依赖注入的实例对象一致，可是使用全局的AutofacContainer获取到的服务实例与依赖注入的实例对象不一致，建议使用IServiceProvider和IComponentContext获取服务实例。

### 6-2-10>一个接口，多个实现的服务注册解决方案参考下面文章

https://www.cnblogs.com/netcs/p/12889834.html

### 6-2-11>Autofac依赖注入还可以使用json格式的配置文件实现，参考https://www.limitcode.com/detail/5f1406baed56b80fe4cc1d0a.html

```C#
{
  "defaultAssembly": "AspNetCore.Ioc.Interface", //接口所在的程序集名称
  "components": [
    {
      "type": "AspNetCore.Ioc.Service.UserService,AspNetCore.Ioc.Service", //接口的实现 全名称
      "services": [
        {
          "type": "AspNetCore.Ioc.Interface.IUserService" // 接口的全名称
        }
      ],
      "instanceScope": "single-instance", //单例生命周期
      "injectProperties": true //是否支持属性注入
    },
    {
      "type": "AspNetCore.Ioc.Service.ProductService,AspNetCore.Ioc.Service", //接口的实现 全名称
      "services": [
        {
          "type": "AspNetCore.Ioc.Interface.IProductService" // 接口的全名称
        }
      ],
      "instanceScope": "single-instance", //单例生命周期
      "injectProperties": true //是否支持属性注入
    }
  ]
}
protected override void Load(ContainerBuilder builder)
{
    //Autofac 基于配置文件的服务注册
    IConfigurationBuilder configurationBuilder = new ConfigurationBuilder();
    configurationBuilder.AddJsonFile("Config/autofac.json");
    IConfigurationRoot root = configurationBuilder.Build();
    //开始读取配置文件中的内容
    ConfigurationModule module = new ConfigurationModule(root);
    //根据配置文件的内容注册服务
    builder.RegisterModule(module);
}
```





# 7>主机

## 7-1>通用主机(可在控制台等程序, 使用依赖注入, 配置, 日志等功能)

### 7-1-1>参考

https://www.cnblogs.com/hopesun/p/12247674.html
https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1
https://www.cnblogs.com/jionsoft/p/12154519.html
https://www.cnblogs.com/jionsoft/p/12164480.html
https://www.cnblogs.com/edison0621/p/11025310.html
*https://www.cnblogs.com/MrHSR/p/10320694.html
https://www.cnblogs.com/zuowj/p/11107243.html

### 7-1-2>.NetCore中的IHostedService

https://www.cnblogs.com/uoyo/p/12377645.html
https://www.cnblogs.com/catcher1994/p/9961228.html
https://www.cnblogs.com/tianyamoon/p/10094802.html

### 7-1-3>以下demo实现了控制台的主机优雅写法，并实现了简单的定时功能。

```C#
/// <summary>
/// 入口
/// </summary>
/// <param name="args">传入参数</param>
/// <returns></returns>
public static async Task Main(string[] args)
{
	await CreateHostBuilder(args).UseConsoleLifetime().Build().RunAsync();
	//下面的方法等同于上面
	//await CreateHostBuilder(args).RunConsoleAsync();
}

/// <summary>
/// 创建泛型主机
/// </summary>
/// <param name="args">传入参数</param>
/// <returns></returns>
public static IHostBuilder CreateHostBuilder(string[] args) =>
	Host.CreateDefaultBuilder(args)
		.ConfigureHostConfiguration(configurationBuilder =>
		{
			configurationBuilder.SetBasePath(FramePublicFun.GetDllPath());
			configurationBuilder.AddJsonFile(SysContant.Hostsettings_FileName, optional: true, reloadOnChange: true);
			configurationBuilder.AddEnvironmentVariables(prefix: SysContant.Setting_Prefix);
			configurationBuilder.AddCommandLine((args ?? new string[] { }));
		})
		.ConfigureAppConfiguration((hostBuilderContext, configurationBuilder) =>
		{
			Console.WriteLine($"hostBuilderContext.HostingEnvironment.EnvironmentName:{hostBuilderContext.HostingEnvironment.EnvironmentName}");

		configurationBuilder.AddJsonFile(SysContant.Appsettings_FileName, optional: true, reloadOnChange: true);

		var appsettingsFileNameArr = SysContant.Appsettings_FileName.Split(new[] { "." }, StringSplitOptions.RemoveEmptyEntries) ?? new string[] { };
		var appsettingsFileNamePrefix = appsettingsFileNameArr.Length != 2 ? "appsettings" : appsettingsFileNameArr[0];
		var appsettingsFileNameExtension = appsettingsFileNameArr.Length != 2 ? "json" : appsettingsFileNameArr[1];
		configurationBuilder.AddJsonFile
		(
			$"{appsettingsFileNamePrefix}.{hostBuilderContext.HostingEnvironment.EnvironmentName}.{appsettingsFileNameExtension}",
			optional: true, reloadOnChange: true
		);

		configurationBuilder.AddEnvironmentVariables(prefix: SysContant.Setting_Prefix);

		configurationBuilder.AddCommandLine(args);
	})
	.ConfigureLogging((hostBuilderContext, loggingBuilder) =>
	{
		loggingBuilder.AddFilter("System", LogLevel.Warning);
		loggingBuilder.AddFilter("Microsoft", LogLevel.Warning);

		var cfgFilePath = Path.Combine(FramePublicFun.GetDllPath(), SysContant.Log4Net_CfgFileName);
		loggingBuilder.AddLog4Net(cfgFilePath);
	})
	//.ConfigureServices((hostBuilderContext, services) =>
	//{
	//    services.AddHostedService<MonitorServerService>();
	//    services.AddHostedService<SeveralTimesPerDayService>();
	//});
	.UseHostedService<MonitorServerService>()
	.UseHostedService<SeveralTimesPerDayService>();
```

*个人对Task.CompletedTask/Task.FromResult 和 Task.Run 的理解
Task.CompletedTask/Task.FromResult是为了返回Task类型, 使用这两个的所在逻辑, 实际是同步执行的, 而Task.Run是确实单独开了一个线程, 异步执行逻辑.
因此, 比如某个接口定义了Task方法, 可是在实现类实现的时候, 发现方法的业务逻辑很简单, 就没必要使用Task.Run, 可以直接使用Task.CompletedTask/Task.FromResult.

## 7-2>Web主机(在3.x版本)

主机配置独立出了web主机配置, ConfigureWebHostDefaults, 跟web主机相关的配置, 如Configure.

### 7-2-1>Kestrel的配置, 可以在ConfigureWebHostDefaults内使用webBuilder.ConfigureKestrel配置, 也可以在ConfigureServices里加载配置文件.

```C#
services.Configure<KestrelServerOptions>(Configuration.GetSection("Kestrel"))
```



### 7-2-2>kestrelServerOptions.Limits.MaxRequestBodySize = null; //这个配置用于设置请求正文允许请求的大小, null为不限制大小。也可以在控制器的Action上, 使用[RequestSizeLimit(100000000)]来为每个Action指定不同的允许请求大小.

### 7-2-3>Kestrel其他配置参考官网https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1#kestrel-options.





# 8>配置 & 选项

https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/configuration/?view=aspnetcore-3.1
https://www.cnblogs.com/MrHSR/p/10281426.html
https://www.cnblogs.com/MrHSR/p/10285906.html
https://www.cnblogs.com/guzhanyu/p/9004063.html
https://www.tnblog.net/aojiancc/article/details/3239
https://www.tnblog.net/%E7%A0%81%E5%86%9C%E6%80%9D%E7%91%9E%E4%B8%8D%E5%A7%93%E5%BC%A0/article/details/6243

## 8-1> 配置来源提供程序的顺序

1. 文件 (appsettings.json, appsettings.{Environment}.json, 其中{Environment}是应用的当前托管环境)
2. Azure 密钥保管库
3. 用户机密(Secret Manager) (仅限开发环境中)
4. 环境变量
5. 命令行参数
   通常的做法是将命令行配置提供程序置于一系列提供程序的末尾, 以允许命令行参数替代由其他提供程序设置的配置. 在使用 CreateDefaultBuilder 初始化新的 WebHostBuilder 时，将使用此提供程序序列.

## 8-2>配置约定

1) 配置来源中的键有以下约定:
   键不区分大小写, 比如用GetSection读取时, 可以不管大小写;
   配置来源中设置相同键的值, 则取配置来源中键上设置的最后一个值. 比如appsettings.json与appsettings.{Environment}.json多个配置来源文件;
   分层键, 如在json文件中多个节点, 冒号分隔符(:)适用于所有平台. 而在环境变量的来源配置中, 所有平台均支持采用双下划线 (__);
   ConfigurationBinder 支持使用配置键中的数组索引将数组绑定到类对象;
2) 配置值采用以下约定：
   值是字符串;
   NULL值不能存储在配置中或绑定到对象;

## 8-3>获取配置值的几种方式

(先通过依赖注入获取IConfiguration Configuration)

### 8-3-1>直接获取

```C#
var lifetime = Configuration["Logging:LogLevel:Microsoft.Hosting.Lifetime"];
var dbType = Configuration.GetSection("DBConnectionInfo").GetValue("DBType", "MySQL");
var connStr = Configuration.GetValue("DBConnectionInfo:ConnStr", "EmptyConnStr");
var noExistKey = Configuration.GetValue("DBConnectionInfo:NoKey", "DefaultValue");
```

**一定要注意, 直接获取的方式只能获取到最底层key的值, 如果查询的key对应的值是object或者list, 那么返回值都是空!!!

### 8-3-2>实例化实体获取

```C#
/// <summary>
/// 用于承载配置项
/// </summary>
public class DBConnectionInfo
{
	/// <summary>
	/// 必须有公开的无参构造函数
	/// </summary>
	public DBConnectionInfo()
	{

}

/// <summary>
/// 需要设置get;set;
/// </summary>
public string Version { get; set; } = "5.3";
public string DBType { get; set; }
public string ConnStr { get; set; }

}

var dbConnectionInfo1 = new DBConnectionInfo();
Configuration.GetSection("DBConnectionInfo").Bind(dbConnectionInfo1);
//获取用Get<>
var dbConnectionInfo2 = Configuration.GetSection("DBConnectionInfo").Get<DBConnectionInfo>();
```

### 8-3-3>在ConfigureServices使用services.Configure<T>(Configuration.GetSection(""))来注册配置, 后续可使用IOptions<T> options来获取依赖注入的配置对象, 可以将所有的配置抽到拓展方法类中统一管理.

*比如在appsettings.{Environment}.json的根节点上设置设置一个key(SystemConfig), 将系统所有的参数配置在这个key底下, 然后通过依赖注入, 再后续的其他地方使用. 结合IOptionsSnapshot, 可以实现当配置文件修改后, 马上获取到新的值.
另外,需要修改后马上生效的文件,reloadOnChange一定要设置成true.

```c#
/// <summary>
/// ServiceCollection拓展
/// </summary>
public static class ServiceCollectionExtension
{
	/// <summary>
	/// 添加自定义配置
	/// </summary>
	/// <param name="serviceCollection">服务集合</param>
	/// <param name="configuration">配置对象</param>
	/// <returns></returns>
	public static IServiceCollection AddCustomConfig(this IServiceCollection serviceCollection, IConfiguration configuration)
	{
		if (serviceCollection == null)
		{
			throw new ArgumentNullException(nameof(serviceCollection));
		}

	if (configuration == null)
	{
		throw new ArgumentNullException(nameof(configuration));
	}

	return serviceCollection.Configure<SystemConfig>(configuration.GetSection(nameof(SystemConfig)));
	//return serviceCollection.Configure<SystemConfig>(configuration.GetSection(SysContant.Configuration_Section_SystemConfig));
}

}
/// <summary>
/// 系统配置
/// </summary>
public IOptions<SystemConfig> SystemConfigOption { get; set; }
public IOptionsSnapshot<SystemConfig> SystemConfigOption { get; set; }
```

获取对象配置对象值 SystemConfigOption.Value

### 8-3-4>IOptions<TOptions>, IOptionsSnapshot<TOptions>, IOptionsMonitor<TOptions>

https://www.cnblogs.com/mq0036/p/14552315.html
https://www.cnblogs.com/wenhx/p/ioptions-ioptionsmonitor-and-ioptionssnapshot.html
https://blog.csdn.net/u011473324/article/details/108768675

IOptions<>是全局单例, 因此一旦生成了, 除非通过代码的方式更改, 否则它的值是不会更新的.
IOptionsMonitor<>也是单例, 但是它通过IOptionsChangeTokenSource<> 能够和配置文件一起更新, 也能通过代码的方式更改值.
IOptionsSnapshot<>是范围, 所以在配置文件更新的下一次访问, 它的值会更新, 但是它不能跨范围通过代码的方式更改值, 只能在当前范围（请求）内有效.(在web环境下,每次请求, 重新读取一次配置文件).

## 8-4>环境变量配置

通用主机变量：https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1
Web主机变量: https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1

## 8-5>命令行参数

### 8-5-1>配置自变量示例

```powershell
dotnet run CommandLineKey1=value1 --CommandLineKey2=value2 /CommandLineKey3=value3
dotnet run --CommandLineKey1 value1 /CommandLineKey2 value2
dotnet run CommandLineKey1= CommandLineKey2=value2
```



### 8-5-2>key交换映射

交换映射字典键规则：(1)交换必须以单划线 (-) 或双划线 (--) 开头 。(2) 交换映射字典不得包含重复键。

```C#
public static readonly Dictionary<string, string> _switchMappings = 
	new Dictionary<string, string>
	{
		{ "-CLKey1", "CommandLineKey1" },
		{ "-CLKey2", "CommandLineKey2" }
	};
config.AddCommandLine(args, _switchMappings);
```



## 8-6>文件配置提供程序AddJsonFile(常用), AddIniFile, AddXmlFile

## 8-7>Key-per-file 配置提供程序 AddKeyPerFile(没用过), 需要可以参考: https://www.cnblogs.com/MrHSR/p/10285906.html



## 8-8>内存配置提供程序AddInMemoryCollection

```C#
/// <summary>
/// 构建内存对象的键值对
/// </summary>
public static readonly Dictionary<string, string> _dict =
new Dictionary<string, string>
{
	{"MemoryCollectionKey1", "value1"},
	{"MemoryCollectionKey2", "value2"}
};
config.AddInMemoryCollection(_dict);
```



## 8-9>配置常用读取方法(GetValue、GetSection、GetChildren 和 Exists)

### 8-9-1>GetValue

ConfigurationBinder.GetValue<T> 从具有指定键的配置中提取一个值，并将其转换为指定类型。 
如果未找到该键，则重载允许你提供默认值。
以下示例使用键 NumberKey 从配置中提取字符串值，键入该值作为 int，并将值存储在变量 intValue 中。 如果在配置键中找不到 NumberKey，则 intValue 会接收 99 的默认值。
var intValue = config.GetValue<int>("NumberKey", 99);

### 8-9-2>GetSection

IConfiguration.GetSection 使用指定的子节键提取配置子节。GetSection 永远不会返回 null。 如果找不到匹配的节，则返回空 IConfigurationSection。

### 8-9-3>GetChildren

```json
{ 
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  },
  "section2": {
    "subsection0" : {
      "key0": "value",
      "key1": "value"
    },
    "subsection1" : {
      "key0": "value",
      "key1": "value"
    }
  }
}
```

//在上面的json结构中，获取section2下面的子节点

```C#
var configSection = _config.GetSection("section2");
var children = configSection.GetChildren();
```



### 8-9-4>Exists

//在上面的json结构中，确定配置节是否存在, 为false，是因为配置数据中没有 section2:subsection2 节点

```C#
var sectionExists = _config.GetSection("section2:subsection2").Exists();
```



## 8-10>自定义配置提供程序

用实体框架 (EF) 创建从数据库读取配置键值对的基本配置提供程序(参考官方例子)
https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/configuration/?view=aspnetcore-5.0





# 9>路由

## 9-1>MVC框架路由

### 9-1-1>设置路由中间件

```c#
app.UseMvc(routes =>
{
	routes.MapRoute
	(
		name: "default",
		template: "{controller=Home}/{action=Index}/{id?}"
	);
});
```

等效于

```C#
app.UseMvcWithDefaultRoute();
```

### 9-1-2>传统路由

*传统路由格式：{controller=Home}/{action=Index}/{id?}

*可以添加多个路由映射, 系统按添加顺序进行处理, 因此在此示例中, 将先尝试 blog 路由, 再尝试 default 路由.

```C#
app.UseMvc(routes =>
{
	routes.MapRoute
	(
		"blog", 
		"blog/{*article}",
		defaults: new
		{ 
			controller = "Blog", 
			action = "Article" 
		}
	);
	routes.MapRoute("default", "{controller=Home}/{action=Index}/{id?}");
});
```

*action操作的区分
在处理url请求时, 当通过路由匹配到一个控制器内两项相同的action名称时, mvc必须进行区分, 解决方案是将要提交的action加上 Http 谓词为 POST. 这样post过来时, 就会选择Edit(int, Product).

```C#
public class ProductsController : Controller
{
	public IActionResult Edit(int id) {}

	[HttpPost]
	public IActionResult Edit(int id, Product product) {}
}
```

### 9-1-3>属性路由

```C#
[Route("")]
[Route("Blog")]
[Route("Blog/ArticleList")]
public IActionResult Article()
{
	return View();
}
```

*使用 Http[Verb] 属性的属性路由

```C#
HttpGet("/products")]
public IActionResult ListProducts(){}
[HttpPost("/products")]
public IActionResult CreateProduct(){}
```

*路由合并
若要使属性路由减少重复, 可将控制器Controller上的路由属性与各个操作Action上的路由属性合并.
控制器上定义的所有路由模板均作为操作上路由模板的前缀. 一旦在控制器上放置路由属性, 则控制器中的所有操作都需要使用属性路由.

```C#
[Route("Home")]
public class HomeController : Controller
{
	[Route("")]      // Combines to define the route template "Home"
	[Route("Index")] // Combines to define the route template "Home/Index"
	[Route("/")]     // Doesn't combine, defines the route template ""
	public IActionResult Index()
	{
	}
}
```

*属性路由参数约束

```C#
[HttpGet("Blog/{id}", Name = "Blog_GetArticle")]
[HttpGet("Blog/GetArticle/{id:int}")]
public IActionResult GetArticle(int id)
{
	return Json(new
	{
		Name = $"Article:{id}"
	});
}
```

*自定义路由属性

```C#
public class MyApiControllerAttribute : Attribute, IRouteTemplateProvider
{
	//实现接口的三个属性，这里的[controller]是一个标记替换。
	public string Template => "api/[controller]/{action}/{id?}";
	public int? Order { get; set; }
	public string Name { get; set; }
}    

public class ProductsApiController : Controller
{
	// GET api/values/5
	//  [HttpGet("{id}")]
	[MyApiController()]
	public string Get(int id)
	{
		return "value";
	}
}
```

通过访问url: http://localhost:30081/api/ProductsApi/get/1 来调用get方法.

### 9-1-4>用代码的方式控制URL

#### 9-1-4-1>传统路由下的url生成

Url.Action配合各种参数, 用于生成url.

```C#
[Route("/")]
[HttpGet("Blog/TestUrlFunc")]
public IActionResult TestUrlFunc() 
{
	//var url = Url.Action("TestOptions", "Home");
	var url = Url.Action("GetArticle", new { id = 10 });
	return Json(new
	{
		Name = "HttpGet TestUrlFunc",
		url
	});
}
```

*Redirect 和 RedirectToAction 用于跳转到页面.

```C#
[HttpGet("Blog/Jump2Page")]
public IActionResult TestJump2OtherPage()
{
	//return Redirect("/Home/TestConfig");
	return RedirectToAction("TestConfig", "Home");
}
```

### 9-1-5>area 区域路由

```C#
app.UseEndpoints(endpointRouteBuilder =>
{
	//endpointRouteBuilder.MapControllerRoute
	//(
	//    name: "blog",
	//    pattern: "blog/{*article}",
	//    defaults:new
	//    {
	//        controller = "Blog",
	//        action = "Article"
	//    }
	//);

	endpointRouteBuilder.MapAreaControllerRoute
	(
		name: "github_blog",
		areaName: "GithubBlog",
		pattern: "github/{controller}/{action}/{id?}"
	);

	endpointRouteBuilder.MapControllerRoute
	(
		name: "default",
		pattern: "{controller=Home}/{action=index}/{id?}"
		//pattern: "{controller}/{action}/{id?}"
	);
});

[Area("GithubBlog")]
public class BlogController : BaseController
{

}
```

### 9-1-6>IActionConstraint 路由约束

在下面的示例中, 约束基于路由数据中的国家/地区代码选择操作, 开发人员负责实现Accept方法，当路由中id值为en-US时Accept方法返回true以表示该操作是匹配项, 一切按正常解析返回客户端. 如果Accept方法返回false将不执行IActionConstraint标记的action, 向客户端返回404错误.

```C#
//定义ActionConstraint属性约束
public class CountrySpecificAttribute : Attribute, IActionConstraint
{
	private readonly string _countryCode;

	public CountrySpecificAttribute(string countryCode)
	{
		_countryCode = countryCode;
	}

	public int Order
	{
		get
		{
			return 0;
		}
	}

	public bool Accept(ActionConstraintContext context)
	{
		return string.Equals(
			context.RouteContext.RouteData.Values["id"].ToString(),
			_countryCode,
			StringComparison.OrdinalIgnoreCase);
	}
}

//应用路由的action约束，并且路由中id值为en-US
[CountrySpecific("en-US")]
public IActionResult Privacy(string countryCode)
{
	return View();
}
```

## 9-2>Razor框架路由(基本做的项目是前后端分离, 想了解的可以参考 https://www.cnblogs.com/MrHSR/p/10265458.html)



# 10>错误处理

## 10-1>配置开发环境异常页

```C#
if (env.IsDevelopment())
{
	//注意: 调用该方法，要放在对其捕获异常的任何中间件前面
	app.UseDeveloperExceptionPage();
}
```

## 10-2>配置自定义异常处理页

配置自定义异常处理页,用于非 `Development` 环境下, 下面是razor项目中的异常处理页代码(Pages下Error.cshtml页面).

```C#
if (env.IsDevelopment())
{
	app.UseDeveloperExceptionPage();
}
else
{
	app.UseExceptionHandler("/error");
}
```

## 10-3>配置状态代码页

```C#
//请求处理中间件之前调用 
app.UseStatusCodePages();
```

## 10-4>UseStatusCodePagesWithRedirects重定向

该中间件作用是: (1)向客户端发送302状态码; (2)将客户端重定向到 URL 模板中的位置.

```C#
/当没有正文的响应时, 重定向到指定页面, {0}表示请求出错的http的状态码
app.UseStatusCodePagesWithRedirects("/error/{0}");
```











































