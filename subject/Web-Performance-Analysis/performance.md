## 前端性能-综述

> 作者：赵鑫晖
> 审阅：

第一次仔细的思考前端性能问题，是在一次面试的时候，被问到我对于优化JavaScript性能有哪些了解。我发现我对这个问题并没有系统的了解。所以这个文档是对前端性能问题做一些分类和导引。

### 前端性能问题的分类

在分析前端性能问题之前，我们需要知道，前端页面的特殊性。

前端属于**B/S架构**。HTML、JS、CSS等资源需要从服务端通过网络传输过来，然后渲染在页面上。这首先要求我们**了解HTTP协议**，这样我们可以根据HTTP协议的请求优化传输的速度。然后我们要**了解浏览器渲染页面的原理**，这样我们就可以有根据的来优化HTML中一些可控的部分。当然除了这些，我们还可以控制资源加载的先后顺序，让重要的资源首先加载。

在页面加载完成之后，浏览器开始运行JavaScript脚本，这个时候JavaScript脚本中如果存在效率很低的代码，就会拖慢**页面可交互时间节点**的到来（因为页面交互逻辑大多写在JavaScript中，当然我们也要注意，能用CSS写的交互可以用CSS实现，这样可以加速可交互时间点的到来）。

当JavaScript加载完成之后，用户开始和页面交互。这个时候我们就要优化页面交互相关的代码，以及动画相关的代码，使得用户在交互过程中，一直保持流畅。所谓流畅就是浏览器一秒钟可以渲染60次。

最后，从整个应用的角度来说，我们可以通过使用前端框架，来优化复杂UI中DOM操作的数量（因为DOM操作是页面交互中的性能瓶颈之一）。这部分相对来说不是那么重要，因为主要的工作是由框架完成的。

由此，我们分析了服务端接收到请求，返回HTML文件开始，到浏览器渲染页面，到用户和页面交互这个流程中，不同阶段对于性能的关注点。我们对前端页面性能的不同分类正是由这个过程串联起来的。我们优化不同阶段的性能，最终使整个应用的用户体验有了提升。

前端性能优化的目的，是为了提高用户体验。因此我们追求的是，使得前端页面尽快达到可交互的状态，而不是一味的追求所有资源的快速加载。这个原则是需要我们牢记在心的。


#### 页面加载性能（HTTP请求返回->HTML文件渲染）

+ 如果评价前端加载性能？如何去测量这个性能？（关键指标：First Meaningful Paint时间，关键是页面尽早的达到可交互状态，而不是盲目的要求所有的资源都在第一时间加载）
+ 理解浏览器渲染页面的过程，从而优化HTML markup中一些标签的属性和摆放位置问题。
+ 什么是CDN？CDN的作用是什么？
+ HTTP中的缓存以及浏览器的缓存策略。
+ HTTP中涉及请求并发的部分。
+ 常规优化策略：压缩，减少请求等等。
+ 高级优化策略：PWA。（PWA优化的不仅仅是First Meaningful Paint，也提高了离线体验）
+ 高级优化策略：懒加载。
+ 高级优化策略：CDN图片懒加载。
+ HTTP2介绍。

#### JavaScript性能（JavaScript执行）

+ 常规优化：不要使用eval和with、缓存变量等等。
+ apply和call之间的差别。
+ 如何去精准评估不同方案的性能（Benchmark，跑分）。
+ 如果发现内存泄露问题，如何预防？
+ V8相关的优化。

#### 页面交互性能优化&&动画性能优化（用户与页面交互）

+ 了解浏览器中UI线程、Event Loop的工作原理。（引出16ms这个时间）
+ 节流等，优化交互事件的频率。
+ 不做同步操作，不堵塞UI线程。
+ 长列表渲染优化。

#### 应用级性能优化

+ 减少DOM操作——Virtual DOM
+ 减少DOM操作——异步刷新队列（Async Batch Queue）
