# 数据接口格式
## xml

## yaml

## json

## protobuf





Json

    human readable/editable
    can be parsed without knowing schema in advance
    excellent browser support
    less verbose than XML

XML

    human readable/editable
    can be parsed without knowing schema in advance
    standard for SOAP etc
    good tooling support (xsd, xslt, sax, dom, etc)
    pretty verbose

Protobuf

    very dense data (small output)
    hard to robustly decode without knowing the schema (data format is internally ambiguous, and needs schema to clarify)
    very fast processing
    not intended for human eyes (dense binary)

All have good support on most platforms.

Personally, I rarely use XML these days. If the consumer is a browser or a public API I tend to use json. For internal APIs I tend to use protobuf for performance.

# 数据格式
## 结构化数据
结构化数据可以使用关系型数据库来表示和存储，如MySQL、Oracle、SQL Server等，表现二维形式的数据。可以通过固有键值获取相应信息。一般特点是：数据以行为单位，一行数据表示一个实体的信息，每一行数据的属性是相同的。结构化的数据的存储和排列是很有规律的，这对查询和修改等操作很有帮助。但是，显然，它的扩展性不好（比如，我希望增加一个字段）。
## 非结构化数据
非结构化数据,就是没有固定结构的数据，包含全部格式的办公文档、文本、图片、XML、HTML、各类报表、图像和音频/视频信息等等。一般直接整体进行存储，而且一般存储为二进制的数据格式
## 流式数据
流式数据，特点就是，像流水一样，不是一次过来而是一点一点“流”过来。而你处理流式数据也是一点一点处理。如果是全部收到数据以后再处理，那么延迟会很大，而且在很多场合会消耗大量内存。

流数据是指由数千个数据源持续生成的数据，通常也同时以数据记录的形式发送，规模较小（约几千字节）。流数据包括多种数据，例如客户使用您的移动或 Web 应用程序生成的日志文件、网购数据、游戏内玩家活动、社交网站信息、金融交易大厅或地理空间服务，以及来自数据中心内所连接设备或仪器的遥测数据。

此类数据需要按记录或根据滑动时间窗口按顺序进行递增式处理，可用于多种分析，包括关联、聚合、筛选和取样。借助此类分析得出的信息，公司得以深入了解其业务和客户活动的方方面面，例如服务使用情况（用于计量/计费）、服务器活动、网站点击量以及设备、人员和实物的地理位置，从而迅速对新情况做出响应。例如，公司可以持续分析社交媒体流，从而跟踪公众对其品牌和产品的看法的变化，并在必要时及时做出反应。

https://aws.amazon.com/cn/streaming-data/
