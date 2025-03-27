
### 1. 核心组件

#### 1.1 日志级别管理 (<mcfile name="Level.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\Level.hpp"></mcfile>)
- 定义了五个日志级别：DEBUG、INFO、WARN、ERROR、FATAL
- 提供日志级别到字符串的转换功能

#### 1.2 日志消息格式化 (<mcfile name="Message.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\Message.hpp"></mcfile>)
- 封装日志消息结构
- 包含：时间戳、日志级别、文件名、行号、线程ID等信息
- 提供消息格式化功能

#### 1.3 异步缓冲区 (<mcfile name="AsyncBuffer.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\AsyncBuffer.hpp"></mcfile>)
- 实现了生产者-消费者模型
- 支持动态扩容
- 使用读写位置指针管理缓冲区

#### 1.4 日志输出策略 (<mcfile name="LogFlush.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\LogFlush.hpp"></mcfile>)
提供三种输出方式：
1. `StdoutFlush`: 标准输出
2. `FileFlush`: 文件输出
3. `RollFileFlush`: 滚动文件输出（支持按大小切割）

#### 1.5 日志管理器 (<mcfile name="Manager.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\Manager.hpp"></mcfile>)
- 采用单例模式
- 管理多个日志器实例
- 提供默认日志器

### 2. 配置管理

通过 <mcfile name="config.conf" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\config.conf"></mcfile> 进行配置：
```json
{
    "buffer_size": 10000000,       // 缓冲区基础大小
    "threshold": 10000000000,      // 扩容阈值
    "linear_growth": 10000000,     // 线性增长大小
    "flush_log": 2,               // 刷盘策略
    "backup_addr": "47.116.74.254", // 备份地址
    "backup_port": 8080,          // 备份端口
    "thread_count": 3             // 线程池大小
}
```

### 3. 特色功能

1. **异步写入**：
   - 使用缓冲区实现异步写入
   - 支持缓冲区动态扩容

2. **多级日志**：
   - 支持不同日志级别
   - 可配置不同输出策略

3. **备份功能**：
   - ERROR和FATAL级别日志支持远程备份
   - 使用线程池处理备份任务

4. **文件管理**：
   - 支持日志文件滚动
   - 支持按大小切割日志文件

### 4. 使用方式

通过 <mcfile name="MyLog.hpp" path="e:\Share\Kama-AsynLogSystem-CloudStorage\log_system\logs_code\MyLog.hpp"></mcfile> 提供简单的宏接口：
```cpp
LOGDEBUGDEFAULT(fmt, ...)  // 使用默认日志器
Debug(fmt, ...)           // 自定义日志器
```

### 5. 设计模式应用

1. **单例模式**：日志管理器
2. **工厂模式**：日志输出策略创建
3. **策略模式**：不同的日志输出方式
4. **建造者模式**：日志器的创建

这是一个设计完善的异步日志系统，既保证了性能，又提供了灵活的配置选项。
