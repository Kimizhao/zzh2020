# 使用DotNetty LengthFieldBasedFrameDecoder定长解码器处理TCP粘包

参数说明:

maxFrameLength：解码的帧的最大长度

lengthFieldOffset：长度字段的偏差(长度属性的起始位（偏移位），包中存放有整个大数据包长度的字节，这段字节的其实位置)

lengthFieldLength：长度字段占的字节数(即存放整个大数据包长度的字节所占的长度)

lengthAdjustmen：添加到长度字段的补偿值(长度调节值，在总长被定义为包含包头长度时，修正信息长度)。

initialBytesToStrip：从解码帧中第一次去除的字节数(跳过的字节数，根据需要我们跳过lengthFieldLength个字节，以便接收端直接接受到不含“长度属性”的内容)

failFast ：为true，当frame长度超过maxFrameLength时立即报TooLongFrameException异常，为false，读取完整个帧再报异常

### 协议处理

22 JTNEPackage数据体长度所在的位置

2  JTNEPackage数据体长度占两个字节

1  JTNEPackage校验位

``` c#
channel.Pipeline.AddLast("TcpDecoder", new LengthFieldBasedFrameDecoder(int.MaxValue, 22, 2, 1, 0));
```



### TCP客户端初始化

```
var group = new MultithreadEventLoopGroup();
                var bootstrap = new Bootstrap();
                bootstrap.Group(group)
                 .Channel<TcpSocketChannel>()
                 .Option(ChannelOption.TcpNodelay, true)
                 .Handler(new ActionChannelInitializer<ISocketChannel>(channel =>
                 {
                     IChannelPipeline pipeline = channel.Pipeline;
                     pipeline.AddLast("TcpDecoder", new LengthFieldBasedFrameDecoder(int.MaxValue, 22, 2, 1, 0));
                     pipeline.AddLast("TcpBuffer", new TcpDecoder());
                     pipeline.AddLast(new ClientConnectionHandler(bootstrap, channeldic, logindic, loggerFactory));
                 }));
```

**注意下面这句要放最后**

```c#
pipeline.AddLast(new ClientConnectionHandler(bootstrap, channeldic, logindic, loggerFactory));
```



参考：

[Netty解决粘包和拆包问题的四种方案](https://www.cnblogs.com/AIPAOJIAO/p/10631551.html)

