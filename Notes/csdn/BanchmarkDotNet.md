![image-20200519105915303](I:\z2.repos\zhaozh\zzh2020\Notes\img\image-20200519105915303.png)



```powershell

                     Method | Runtime |     Toolchain |     N |       Mean |     Error |    StdDev | Gen 0/1k Op | Gen 1/1k Op | Gen 2/1k Op | Allocated Memory/Op |
--------------------------- |-------- |-------------- |------ |-----------:|----------:|----------:|------------:|------------:|------------:|--------------------:|
 JTNE_0x02_Device_Serialize |     Clr |       Default |   100 |   8.274 ms | 0.0523 ms | 0.0489 ms |    328.1250 |           - |           - |                   - |
      JTNE_0x02_Deserialize |     Clr |       Default |   100 |   7.305 ms | 0.1101 ms | 0.1029 ms |    343.7500 |           - |           - |                   - |
 JTNE_0x02_Device_Serialize |    Core | .NET Core 2.2 |   100 |   6.702 ms | 0.0585 ms | 0.0547 ms |    289.0625 |           - |           - |            919200 B |
      JTNE_0x02_Deserialize |    Core | .NET Core 2.2 |   100 |   5.899 ms | 0.0635 ms | 0.0594 ms |    304.6875 |           - |           - |            970400 B |
 JTNE_0x02_Device_Serialize |     Clr |       Default | 10000 | 819.906 ms | 9.7220 ms | 9.0940 ms |  33000.0000 |           - |           - |                   - |
      JTNE_0x02_Deserialize |     Clr |       Default | 10000 | 768.556 ms | 3.6753 ms | 3.4379 ms |  34000.0000 |           - |           - |                   - |
 JTNE_0x02_Device_Serialize |    Core | .NET Core 2.2 | 10000 | 661.618 ms | 3.2214 ms | 3.0133 ms |  29000.0000 |           - |           - |          91920000 B |
      JTNE_0x02_Deserialize |    Core | .NET Core 2.2 | 10000 | 580.879 ms | 7.0803 ms | 6.6229 ms |  30000.0000 |           - |           - |          97040000 B |

// * Hints *
Outliers
  JTNESerializerContext.JTNE_0x02_Deserialize: Platform=AnyCpu, Runtime=Clr, Server=False -> 1 outlier  was  detected

// * Legends *
  N                   : Value of the 'N' parameter
  Mean                : Arithmetic mean of all measurements
  Error               : Half of 99.9% confidence interval
  StdDev              : Standard deviation of all measurements
  Gen 0/1k Op         : GC Generation 0 collects per 1k Operations
  Gen 1/1k Op         : GC Generation 1 collects per 1k Operations
  Gen 2/1k Op         : GC Generation 2 collects per 1k Operations
  Allocated Memory/Op : Allocated memory per single operation (managed only, inclusive, 1KB = 1024B)
  1 ms                : 1 Millisecond (0.001 sec)

// * Diagnostic Output - MemoryDiagnoser *


// ***** BenchmarkRunner: End *****
Run time: 00:02:39 (159.79 sec), executed benchmarks: 8

// * Artifacts cleanup *

C:\Program Files\dotnet\dotnet.exe (进程 9048)已退出，代码为 0。
按任意键关闭此窗口. . .
```



![image-20200519133154353](I:\z2.repos\zhaozh\zzh2020\Notes\img\image-20200519133154353.png)