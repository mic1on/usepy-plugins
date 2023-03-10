### 一个全局拦截日志并转为loguru日志的插件

<a href="https://pypi.org/project/usepy-plugin-logger" target="_blank">
    <img src="https://img.shields.io/pypi/v/usepy-plugin-logger.svg" alt="Package version">
</a>

<a href="https://pypi.org/project/usepy-plugin-logger" target="_blank">
    <img src="https://img.shields.io/pypi/pyversions/usepy-plugin-logger.svg" alt="Supported Python versions">
</a>

#### 文档

[useLogger | UsePy](https://usepy.code05.com/api/logger.html) 

#### 安装

> pip install usepy-plugin-logger

#### 使用

```python
from usepy.logger import useLogger

useLogger() # 使用默认配置

```

如果你自身项目正在使用`loguru`，这一切似乎感觉毫无变化。因为默认的配置只是修改了一点输出样式。

如果想要感受它带来的“魔法”，需要稍微配置一下。

```python
from usepy.logger import useLogger
useLogger(packages=["scrapy",  "django",  "usepy"]) 

```

##### Logstash/Filebeat

日志的更重要能力是将日志记录发送到`Logstash`/`Filebeat`，这样就可以将日志记录存储到`Elasticsearch`中，方便进行日志分析。所以统一日志的最终输出格式是非常重要的。

`useLogger`内置一个`logstash_handler`统一化输出格式。

```python
from usepy import useTimeIt
from usepy.logger import useLogger, logstash_handler
useLogger(
 handlers=[
 logstash_handler(level="DEBUG",  extra={"app_name":  "spider"})
 ],
 packages=["usepy"],  # hook拦截 usepy 的日志
 extra={"project_name":  "usepy"}
)
logger.warning("test warning")
logger.info("test info")
logger.debug("test debug")

```


