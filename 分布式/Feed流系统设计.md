https://www.youtube.com/watch?v=kAmmSTdIm1E     
what is newsfeed?(消息流可以点赞，评论什么的)      
News Feed is the constantly updating list of stories in the middle of your home pageNews Feed includes status updates, photos, videos links, app activity and likes from people, Pages and groups that you follow on Facebook.         

Normal steps of system design：
1.Requirement clarification     
2.Scale of the system - data size     
3.API interface     
4.database data modle     
5.High-level design(draw a picture)         
6.Detailed design(corner case of user user case.cache, load balance, optimize)      
7.Bottlenecks (single point of failure, replicas ofthe data if lost, monitoring, alart, autofix/ticket)  


第一步根据前面的问答我们需要确定用户的需求，我们的产品的purpose    
Functional requirements:产生朋友圈newsfeed building，看朋友圈feed publishing     
1.产生信息流 generate newsfeed    
2.用户可以订阅别人 (这里可以展开很多，like,comment(comment on a commentlG不允许会只保存2层)         
3.信息流可以文字图片视频 (和票圈一样) get/store image/video/text        
4.用户取信息流，在线用户及时更新 notification/publishing feed     

Non-functional requirements:
对于所有用户信息流快速创建，信息流有新post 5秒内快速传送        
Our system should be able to generate any user's newsfeed in real-time - maximum latency seen bythe end user would be 2s.A post shouldn't take more than 5s to make it to a user's feed assuming a new newsfeed request2      
comes in.    

2. Scale of the system - data size(不太重要)    
我们有300个小伙伴，我们同时订阅了200个公众号     
Traffic estimates:比如我们有30M DAU(Daily Active User),每个用户每天刷10次手机里的newsfeed,最后我们有300M newsfeed request 每天，换算成秒 /86400 =3500 每秒request      
Storage estimates;我们cache保存500个post给每个user，每个post假设简单的texi占用1kb，一个用户50okb，     
30M*500 kb =15000M kb = 15 MMB=内存15TB来做memo cache,一个server保存100GB,那么我们需要150台机器

3. System APIs
1）Feed publishing API        
POST /v1/me/feed        
Params:   
content: content is the text of the post     
user id: 总得告诉server谁发的帖子吧    
auth token:给 gateway request authentication         

2) News feed retrieval API       
GET /v1/me/getAllFeeds           
Params:      
auth token    
user id

当然parameter可以扩展比如只要几号到几号之间的    
优先级权重是什么的 最多要几个post那些不看的 (比如filter掉成人内容的)    
还有一些不重要的比如加好友订阅别人，给别人的票圈点赞评论转发，我们就都忽略了不涉及，大家自己嘴遁一下不要浪费太多时间即可     

4. Database design   
User (用户) => 可以和别的用户好友，可以订阅公众号     
Entity (e.g. page, group, etc.),用户和公众号都可以发文章     
FeedItem (or Post) (一篇微信公众号文章后者一个票圈)我们加个表格记录一下是谁发的    
然后还可以加like table, id, parent, userd, active, timestamp    还可以有comment table

![截屏2024-02-05 11.57.40.png](https://img.xwyue.com/i/2024/02/05/65c0cd3e01a75.png)

细节：    
Feed generation(building)      
把自己订阅的用户ID都拿回来     
通过ID查询出他们最新的post      
根据自己的喜好来post排序，必须我喜欢猫，猫在前面。    
把产生出来的结果放入cache，把最新的20个posts放在newsfeed上展示如果用户已经把这20个看完了，用户小手一抖，一个下拉再从cache里面取下一组20个5     

这里每个用户的20个newsfeed可以用linkedhashmap来保存，既可以o1拿到任何一个post，又可以按照相对顺序排列，下一次读上次遗留下来的位置   

这里注意因为我们是offeline algorithm不是实时的，如果这个用户在线，同时有新的post来我们就需要额外处理加入到这个newsfeed中?   

In the interview, we will also need to discuss in-depth how the feed will be updatedcontinuously with new incoming posts from entities that Mathew follows.      
Possible Solution:       
1. Run the feed generation process periodically (every five minutes) toadd new and popular posts to Mathew's feed       
2. Notify Mathew whenever we have new updates available for him that he can fetch      

Feed publishing:
用户首次登陆，或者用户手动下拉我们来load更多的post
fanout service用来把新post发送给订阅者

这里讨论关于fanout on write vs fanout on read     
fanout process:    
1.use graph database to get user follower ids     
2.get user info from cache, so you can mute one you don't like,或者你不在对方的group里    
3.postId, friend list send to message queue    
4.fanout worker 保存数据到 news feed cache<post id, user_id>有新的来就append     

6.细节设计
"Pull" model or Fan-out-on-load: This model involves keeping recent feed data in memory on the server. It's noted that this approach does not scale well when user numbers are high, leading to potential "hotkey" issues.    

Problem: Every user needs to send a pull request.     
Problem: Continuous polling without updates leads to an empty response, which is inefficient.     

"Push" model or Fan-out-on-write: This involves pushing updates directly to the newsfeed, and can potentially use long polling or websockets.      

Advantage: Real-time updates, reducing the number of requests.    
Problem: High cost when the number of followers is large, leading to a hotkey problem.     

Hybrid: Combines push model for celebrities (likely meaning users with many followers) and pull model for typical users.   

"Hotkey"问题通常是指在分布式系统中，某个特定的键值（key）被过度频繁地访问，导致了不均匀的负载分布。这个术语常用于缓存和数据库优化的上下文中。例如，如果一个热门的内容或者数据项被大量用户同时请求，这个数据项对应的键值就会成为一个"hotkey"。这会导致以下问题：

性能瓶颈：过多的请求集中在少数服务器上，导致这些服务器的负载过高，而其他服务器则可能负载较轻。这会影响整个系统的性能和响应时间。

资源浪费：为了应对可能的高负载，系统可能需要过度地分配资源以保证性能，但这些资源在非高峰时段可能会被浪费。

可用性问题：极端情况下，对"hotkey"的过度请求可能导致服务不可用，影响用户体验。   

常规follow up 无限剑制    
scaling database     
vertical vs horizontal    
sql vs nosq    
master-slave replicas    
consistency models    
database sharding    
keep web tier stateless    
hotkey festival special case handle   



