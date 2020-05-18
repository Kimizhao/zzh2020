# DotNetty IByteBuffer to a byte[]

在做DotNetty客户端数据接收时，buffer中获取。

```c#
    public override void ChannelRead(IChannelHandlerContext context, object message)
    {
        try
        {
            if (message is IByteBuffer buffer)
            {
                Span<byte> spby = ((Span<byte>)buffer.Array).Slice(buffer.ArrayOffset, buffer.ReadableBytes);

                if (logger.IsEnabled(LogLevel.Trace))
                {
                    logger.LogTrace("accept msg<<<" + spby.ToArray().ToHexString());
                }
            }
        }
        catch (Exception ex)
        {
            
        }
        
    }
```
参考：[Converting IByteBuffer to byte[]](//https://github.com/Azure/DotNetty/issues/415)