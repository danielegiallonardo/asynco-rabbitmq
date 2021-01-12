# RabbitMQ remoting transport for Asynco
This transport uses two RabbitMQ queues, one for the requests and one for the replies. In order for the correlation between requests and replies to be achieved, it uses the direct reply-to mechanism as decribed [here](https://www.rabbitmq.com/direct-reply-to.html). Just set it up by using

```csharp
services.AddRemoting(options =>
	options.UseRabbitMQ(opt =>
	{
		// This is used on the sender side, it's the DispatchProxy timeout 
		opt.Timeout = TimeSpan.FromMinutes(1); 
		opt.RequestsQueueName = "<asyncrequestsqueuename>";
		opt.RepliesQueueName = "<asyncrepliesqueuename>";
		opt.HostName = "localhost";
		opt.UserName = "<username>";
		opt.Password = "<password>";
		// Optional, default is 5672
		opt.Port = 5672;
		// Optional, default is string empty
		opt.Exchange = "";
		// Optional, default is 1
		opt.ConsumerDispatchConcurrency = 1;
	}))
```


More on the remoting transports in the Samples.

## Installing via NuGet
`Install-Package Asynco.RabbitMQ`
