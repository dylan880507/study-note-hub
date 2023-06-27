## 1>相关文章

### 1-1>JWT在线解码工具

https://jwt.io/

### 1-2>asp.net core 集成JWT

[asp.net core 集成JWT（一）](https://www.cnblogs.com/7tiny/p/11012035.html)

[asp.net core 集成JWT（二）token的强制失效，基于策略模式细化api权限](https://www.cnblogs.com/7tiny/p/11019698.html)

### 1-3>ASP.NET Core Web Api之JWT

[ASP.NET Core Web Api之JWT(一)](https://www.cnblogs.com/CreateMyself/p/11123023.html)

[ASP.NET Core Web Api之JWT VS Session VS Cookie(二)](https://www.cnblogs.com/CreateMyself/p/11197497.html)

[ASP.NET Core Web Api之JWT刷新Token(三)](https://www.cnblogs.com/CreateMyself/p/11273732.html)

[ASP.NET Core Identity自定义数据库结构和完全使用Dapper而非EntityFramework Core](https://www.cnblogs.com/CreateMyself/p/11291623.html)

### 1-4>ASP.NET Core 实战：基于 Jwt Token 的权限控制全揭露

https://www.cnblogs.com/danvic712/p/10331976.html

### 1-5>用JWT来保护我们的ASP.NET Core Web API

https://www.cnblogs.com/catcher1994/p/6057484.html

### 1-6>用Middleware给ASP.NET Core Web API添加自己的授权验证

https://www.cnblogs.com/catcher1994/p/6021046.html

### 1-7>ASP.NET Core 认证与授权[4]:JwtBearer认证

https://www.cnblogs.com/RainingNight/p/jwtbearer-authentication-in-asp-net-core.html

### 1-8>jwt策略参数

https://www.cnblogs.com/fger/p/12202362.html

### 1-9>Authentication跟Authorization的区别

https://blog.csdn.net/linshunhuang1/article/details/108798219

### 1-10>使用Swagger为.NET Core 3.0应用添加JWT授权说明文档

https://blog.csdn.net/weixin_33008495/article/details/102811347

https://www.cnblogs.com/nwdnote/p/13554202.html

### 1-11>Asp Net Core 5 REST API 使用 RefreshToken 刷新 JWT - Step by Step（三）

https://mp.weixin.qq.com/s?__biz=MzA5NjQ1Njc3Ng==&mid=2247484402&idx=1&sn=264b5235d944f47b250ed478300fcff9



## 2>JWT令牌结构

`*JWT由三部分构成: Base64编码的Header(头), Base64编码的Payload(有效载荷), Signature(签名) 三部分通过点隔开.`



*第一部分以Base64编码的Header主要包括Token的类型和所使用的算法:

```json
{
	"alg": "HS265", //签名算法
	"typ": "JWT" //令牌的类型
}
```

*第二部分以Base64编码的Payload主要包含的是声明(Claims):

 7个官方字段:

- iss (issuer)：签发人
- exp (expiration time)：过期时间
- sub (subject)：主题
- aud (audience)：受众
- nbf (Not Before)：生效时间
- iat (Issued At)：签发时间
- jti (JWT ID)：编号

 可以在这个部分定义私有字段:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

*第三部分则是将Key通过对应的加密算法生成签名, 最终三部分以点隔开:

```powershell
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiSmVmZmNreSIsImVtYWlsIjoiMjc1MjE1NDg0NEBxcS5jb20iLCJleHAiOjE1NjU2MTUzOTgsIm5iZiI6MTU2MzE5NjE5OCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDAwIiwiYXVkIjoiaHR0cDovL2xvY2FsaG9zdDo1MDAxIn0.
OJjlGJOnCCbpok05gOIgu5bwY8QYKfE2pOArtaZJbyI
```

## 3>基础概念

[Claim（每一项的证件信息）=》ClaimsIdentity（证件）=》ClaimsPrincipal（证件持有者）](https://www.cnblogs.com/danvic712/p/10331976.html)



## 4>NET Core中使用JWT

### 4-1>结合JWT认证对用户进行API授权

`自定义鉴权策略逻辑: 策略(PolicyRequirement)保存角色与权限的关系列表, 在PolicyHandler里获取用户当前访问的api路径, 再根据用户所具备的角色, 判断用户是否可以访问当前api.`

```C#
/// <summary>
/// PolicyRequirement
/// </summary>
public sealed class PolicyRequirement : IAuthorizationRequirement
{
	/// <summary>
	/// 角色api权限集合
	/// </summary>
	public List<RoleApiPermission> RoleApiPermissions { get; private set; } = new();

	/// <summary>
	/// 构造函数
	/// </summary>
	public PolicyRequirement()
	{
		//初始化角色api权限集合
		RoleApiPermissions = new List<RoleApiPermission>
		{
			new RoleApiPermission
			{
				Name="SystenAdmin",
				Urls = new HashSet<string>
				{
					"/calc/TestJWT/Action3",
				},
			},
		};
	}
}

/// <summary>
/// RoleApiPermission
/// </summary>
public sealed class RoleApiPermission : RoleApiPermission<long>
{
	/// <summary>
	/// 
	/// </summary>
	public RoleApiPermission() : base()
	{

	}
}

/// <summary>
/// RoleApiPermission
/// </summary>
/// <typeparam name="TKey"></typeparam>
public class RoleApiPermission<TKey>
{
	/// <summary>
	/// Id
	/// </summary>
	public virtual TKey Id { get; set; } = SnowflakeID.GetInstance().GetNextID<TKey>();
	/// <summary>
	/// 名称
	/// </summary>
	public virtual string Name { get; set; }
	/// <summary>
	/// 请求Url
	/// </summary>
	public virtual HashSet<string> Urls { get; set; } = new();
}
```

```C#
/// <summary>
/// 策略处理
/// </summary>
public class PolicyHandler : AuthorizationHandler<PolicyRequirement>
{
	/// <summary>
	/// 处理鉴权策略
	/// </summary>
	/// <param name="context">AuthorizationHandlerContext</param>
	/// <param name="requirement">PolicyRequirement</param>
	/// <returns></returns>
	protected override Task HandleRequirementAsync(AuthorizationHandlerContext context, PolicyRequirement requirement)
	{
		if (context.Resource == default) 
		{
			throw new ArgumentNullException(nameof(context.Resource));
		}

		//获取HttpContext
		var httpContext = (context.Resource as Microsoft.AspNetCore.Http.DefaultHttpContext);
		if (httpContext == default)
		{
			throw new ArgumentNullException(nameof(httpContext));
		}
		//请求Url
		var questUrl = httpContext.Request?.Path.Value?.ToLower().TrimAll() ?? "";
		if (questUrl == default)
		{
			throw new ArgumentNullException(nameof(questUrl));
		}

		//是否经过验证
		var isAuthenticated = httpContext.User?.Identity?.IsAuthenticated ?? false;
		if (!isAuthenticated)
		{
			return Task.CompletedTask;
		}

		//获取当前用户的角色列表
		var roleStr = httpContext.User.Claims.FirstOrDefault(c => c.Type == ClaimTypes.Role)?.Value ?? "";
		if (string.IsNullOrEmpty(roleStr))
		{
			throw new InvalidOperationException("Role of user is null!");
		}

		if (!roleStr.TryJArrayParse(out JArray roles))
		{
			throw new InvalidCastException("Format of role is error!");
		}

		if (roles.Count <= 0)
		{
			throw new InvalidOperationException("Role of user is null!");
		}

		var rolePermissions = requirement.RoleApiPermissions;
		if (rolePermissions == default || rolePermissions.Count <= 0)
		{
			throw new InvalidOperationException($"{nameof(rolePermissions)} is null!");
		}

		//有权限
		if (
			(
				requirement.RoleApiPermissions
					.Where(r => roles.Any(jToken => jToken.ToString().TrimAll().ToLower() == r.Name.TrimAll().ToLower())).ToList()
					.SelectMany(r => r.Urls).ToList() ?? new List<string>()
			).Distinct().ToList()
			.Any(url => url.TrimAll().ToLower() == questUrl)
		)
		{
			context.Succeed(requirement);
			return Task.CompletedTask;
		}


		//重定向到无权限页面
		//httpContext.Response.Redirect(requirement.NoPermissionAction);

		//返回无权限的响应结果
		httpContext.Response.Headers.Add
		(
			SysContant.JWT_ResponseHeader_ActualReason, 
			SysContant.ResultMsg_NoPermission
		);
		httpContext.Response.StatusCode = (int)HttpStatusCode.Forbidden;
		context.Fail();
		return Task.CompletedTask;
	}
}
```

```C#
//Startup.ConfigureServices
//添加策略模式的配置
.AddAuthorization(authorizationOptions => 
{
	authorizationOptions.AddPolicy("CustomAuthorization", policy =>
	{
		policy.AddRequirements(new PolicyRequirement());
	});
})
.AddSingleton<IAuthorizationHandler, PolicyHandler>()
```

### 4-2>一个用户同时只能拥有一个有效的Access Token

`实现逻辑:在JWT验证里, 可以开启Issuer, Audience, Token(真实性跟有效性)验证, 因此可以让鉴权服务器生成动态的Audience, 保证每次生成Token的时候, 都加入一个唯一的Audience, 这样, 每个用户(每个AppID)同时只能拥有一个唯一有效的Access Token.`

```C#
/// <summary>
/// Auth
/// </summary>
[Route("calc/[controller]")]
[ApiController]
public class AuthController : ControllerBase
{
	/// <summary>
	/// IMemoryCache
	/// </summary>
	private readonly IMemoryCache _memoryCache = default;

	/// <summary>
	/// <![CDATA[IOptionsSnapshot<SystemConfig>]]> 
	/// </summary>
	private readonly IOptionsSnapshot<SystemConfig> _optionsSnapshot = default;
	/// <summary>
	/// 系统配置
	/// </summary>
	private readonly SystemConfig _systemConfig = default;
	/// <summary>
	/// memoryCache
	/// </summary>
	/// <param name="memoryCache">memoryCache</param>
	/// <param name="optionsSnapshot">optionsSnapshot</param>
	public AuthController(IMemoryCache memoryCache, IOptionsSnapshot<SystemConfig> optionsSnapshot)
	{
		_memoryCache = memoryCache ?? throw new ArgumentNullException(nameof(memoryCache));
		_optionsSnapshot = optionsSnapshot ?? throw new ArgumentNullException(nameof(optionsSnapshot));
		_systemConfig = _optionsSnapshot.Value ?? throw new ArgumentNullException(nameof(_optionsSnapshot.Value));

		//设置全局的MemoryCache
		FramePublicFun.MemoryCacheGlobal = memoryCache;
	}

	/// <summary>
	/// 登录
	/// </summary>
	/// <param name="userName">用户名</param>
	/// <param name="passWord">密码</param>
	/// <param name="cancellationToken">cancellationToken</param>
	/// <returns></returns>
	[HttpPost("Login")]
	public async Task<FunResult> LoginSync(string userName, string passWord, CancellationToken cancellationToken=default)
	{
		try
		{
			userName = userName ?? "";
			passWord = passWord ?? "";
			//TODO 校验用户账号密码
			if (userName != "dylanxu" || passWord != "123456")
			{
				return new FunResult
				(
					SysContant.ResultCode_InvalidUserNameOrPassword,
					"Fail",
					null
				);
			}
			//TODO 查询用户拥有的角色集合
			var roles = new List<string> { "SystenAdmin" };

			var utcNow = DateTimeOffset.UtcNow;
			//创建声明集合
			var claims = new[]
			{
				new Claim
				(
					JwtRegisteredClaimNames.Nbf,
					$"{utcNow.ToUnixTimeSeconds()}"
				) ,
				new Claim
				(
					JwtRegisteredClaimNames.Exp,
					$"{utcNow.AddSeconds(_systemConfig.JWTSetting.Expiration_AccessToken.Value).ToUnixTimeSeconds()}"
				),
				new Claim
				(
					ClaimTypes.Name,
					userName
				),
				//new Claim
				//(
				//  SysContant.ClaimTypes_PassWord,
				//  passWord
				//),
				new Claim
				(
					ClaimTypes.Role,
					NewtonsoftSerializer.SerializeObject(roles)
				),
			};

			//设置动态的audience, 加上SnowID, 保证每个用户, 每次登录后, audience都是唯一的
			//TODO 后期改成用redis缓存
			var cacheKey = $"{SysContant.Cache_Key_Prefix_Audience}{userName}";
			var audience =
				FramePublicFun.MD5
				(
					$"{userName}|^|{passWord}|^|{await SnowflakeID.GetInstance().GetNextIDAsync<string>()}",
					false,
					Encoding.UTF8
				);
			//每个用户的audience缓存失效期可以不设置
			//服务器鉴权时, 先校验的audience, 再校验token是否失效
			//audience的作用主要是为了验证用户是否重新登录了, 或者是否修改了密码, audience的失效期并不重要,
			//因为鉴权服务器会校验token的有效期
			await _memoryCache.SetCacheAsync
				(
					cacheKey, audience,
					TimeSpan.FromSeconds(int.MaxValue),
					default, default,
					cancellationToken
				);

			var symmetricSecurityKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_systemConfig.JWTSetting.SecurityKey));
			var signingCredentials = new SigningCredentials(symmetricSecurityKey, SecurityAlgorithms.HmacSha256);

			var jwtSecurityToken = new JwtSecurityToken
			(
				issuer: _systemConfig.JWTSetting.Issuer,
				audience: audience,
				claims: claims,
				expires: DateTime.UtcNow.AddSeconds(_systemConfig.JWTSetting.Expiration_AccessToken.Value), //控制jwtToken的有效时间
																						 //expires: DateTime.Now.AddMinutes(1), //控制jwtToken的有效时间
				signingCredentials: signingCredentials
			);

			var jwtSecurityTokenHandler = new JwtSecurityTokenHandler();
			var jwtToken = jwtSecurityTokenHandler.WriteToken(jwtSecurityToken);

			return await Task.FromResult(new FunResult
			(
				SysContant.ResultCode_Success,
				"Success",
				jwtToken
			));
		}
		catch (Exception ex)
		{
			return new FunResult
			(
				SysContant.ResultCode_Fail,
				ex.GetInnerExceptionMsg(),
				null
			);
		}
	}
}
```

```C#
//Startup.ConfigureServices
//添加JWT验证
services
	//添加策略模式的配置
	.AddAuthorization(authorizationOptions => 
	{
		authorizationOptions.AddPolicy("CustomAuthorization", policy =>
		{
			policy.AddRequirements(new PolicyRequirement());
		});
	})
	.AddSingleton<IAuthorizationHandler, PolicyHandler>()
	//.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
	.AddAuthentication(authenticationOptions => 
	{
		//添加JWT Scheme
		authenticationOptions.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
		authenticationOptions.DefaultScheme = JwtBearerDefaults.AuthenticationScheme;
		authenticationOptions.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
	})
	.AddJwtBearer(jwtBearerOptions => 
	{
		jwtBearerOptions.Events = new JwtBearerEvents
		{
			//TokenValidated：在Token验证通过后调用。
			//AuthenticationFailed: 认证失败时调用。
			//Challenge: 未授权时调用。
			//设置消息接收事件, 可以自定义Token的获取方式
			OnMessageReceived = messageReceivedContext =>
			{
				var access_token = messageReceivedContext.Request.Headers[SysContant.JWT_AccessToken].ToString();
				if (string.IsNullOrEmpty(access_token))
				{
					access_token = messageReceivedContext.Request.Query[SysContant.JWT_AccessToken].ToString();
				}

				messageReceivedContext.Token = access_token;
				return Task.CompletedTask;
			},
			OnAuthenticationFailed = authenticationFailedContext => 
			{
				//若是token过期, 则在响应头上返回具体原因
				if (authenticationFailedContext.Exception.GetType() == typeof(SecurityTokenExpiredException))
				{
					authenticationFailedContext.Response.Headers.Add
					(
						SysContant.JWT_ResponseHeader_ActualReason,
						SysContant.ResultMsg_TokenExpired
					);
				}

				return Task.CompletedTask;
			},
		};

		//设置令牌校验参数
		jwtBearerOptions.TokenValidationParameters = new TokenValidationParameters
		{
			ValidateIssuer = true, //是否验证Issuer
			ValidIssuer = Configuration["SystemConfig:JWTSetting:Issuer"], //Issuer，这两项和前面签发jwt的设置一致

			ValidateAudience = true, //是否验证Audience
			//ValidAudience = SysContant.JWT_Domain, //Audience
			AudienceValidator = (audiences, securityToken, validationParameters) =>
			{
				var jwtSecurityToken = securityToken as JwtSecurityToken;
				if (jwtSecurityToken == default) 
				{
					//throw new InvalidCastException(nameof(jwtSecurityToken));
					return false;
				}

				var userName = jwtSecurityToken.Claims.FirstOrDefault(c => c.Type == ClaimTypes.Name)?.Value ?? "";
				if (string.IsNullOrEmpty(userName)) 
				{
					//throw new ArgumentNullException(nameof(userName));
					return false;
				}

				if (FramePublicFun.MemoryCacheGlobal == default)
				{
					return false;
				}

				//TODO 从redis中获取当前用户的audience
				var cacheKey = $"{SysContant.Cache_Key_Prefix_Audience}{userName}";
				var (result, val) = FramePublicFun.MemoryCacheGlobal.TryGetVal<string>(cacheKey);
				if (!result)
				{
					return result;
				}
				if (string.IsNullOrEmpty(val))
				{
					return false;
				}

				//校验当前的audiences是否与缓存的相同
				return audiences.Contains(val);
			},
			ValidateLifetime = true, //是否验证Token有效期，使用当前时间与Token的Claims中的NotBefore和Expires对比
			ClockSkew = TimeSpan.FromSeconds(double.Parse(Configuration["SystemConfig:JWTSetting:ClockSkew"])), //允许的服务器时间偏移量

			ValidateIssuerSigningKey = true, //是否验证SecurityKey
			IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Configuration["SystemConfig:JWTSetting:SecurityKey"])) //拿到SecurityKey
		};
	});
```

```C#
//Startup.Configure
app.UseAuthentication()//启动JWT验证
   .UseAuthorization();
```

### 4-3>Swagger启用JWT

```C#
//Startup.ConfigureServices
//注册Swagger
.AddSwaggerGen(swaggerGenOptions =>
{
	swaggerGenOptions
		//Swagger拓展配置
		.ConfigExtension($"{typeof(Startup).Namespace}.xml")
		.SwaggerDoc
		(
			"v1",
			new OpenApiInfo
			{
				Title = "Dylan.DbContextApiDemo",
				Version = "v1"
			}
		);

	//Swagger开启JWT 
	swaggerGenOptions.AddSecurityDefinition(JwtBearerDefaults.AuthenticationScheme, new OpenApiSecurityScheme
	{
		Name = "Authorization",
		In = ParameterLocation.Header,
		Type = SecuritySchemeType.ApiKey,
		BearerFormat = "JWT",
		Scheme = JwtBearerDefaults.AuthenticationScheme,
		Description = "JWT Authorization header using the Bearer scheme. Example: \"Authorization: Bearer {token}\"",
	});
	swaggerGenOptions.AddSecurityRequirement(new OpenApiSecurityRequirement
	{
		{
			new OpenApiSecurityScheme
			{
				Reference = new OpenApiReference
				{
					Type = ReferenceType.SecurityScheme,
					Id = JwtBearerDefaults.AuthenticationScheme
				}
			},new string[]{ }
		}
	});
})
```

```C#
/// <summary>
/// Swagger拓展类
/// </summary>
public static class SwaggerExtension
{
	/// <summary>
	/// Swagger拓展配置
	/// </summary>
	/// <param name="opt">SwaggerGenOptions</param>
	/// <param name="xmlName">xml文件名</param>
	public static SwaggerGenOptions ConfigExtension(this SwaggerGenOptions opt, string xmlName)
	{
		if (opt == default)
		{
			throw new ArgumentNullException(nameof(opt));
		}

		if (string.IsNullOrEmpty(xmlName))
		{
			throw new ArgumentNullException(nameof(xmlName));
		}

		var xmlPath = Path.Combine(FramePublicFun.GetDllPath(), xmlName);
		if (!File.Exists(xmlPath))
		{
			throw new InvalidOperationException($"Fail to locate file ({xmlPath})!");
		}

		opt.IncludeXmlComments(xmlPath);

		return opt;
	}
}
```

### 4-4>通过RefreshToken刷新Token

*`基本概念:`JWT Token有一个过期时间, 时间越短越安全. 过期后，有两种方法可以获取新的 access token:

- 客户端(前端)检测到access token失效后, 重定向到登录页面, 让用户重新登录.
- 使用Refresh Token自动重新验证用户, 并生成新的 access token.



### 4-5>封装





## 5>注意事项

*`签名的SecurityKey长度至少要16位, 否则生成Token会报错.`

*`使用自定义鉴权策略, 只有在class或者method上标识 Authorize(policy: "自定义鉴权策略名称"), 才会走自定义鉴权策略的逻辑.`

