### Now create "acm" using terraform code
We need to validate, aws will check wether we able to create records or not ? in our hosted zones.

### Now start creating web component 08-web-alb
Create web-alb then web component, you need to take latest policy while writing listener which can be seen while creating in aws console which is "ELB Security policy latest which is recommended"

### Now create web component 09-web
You can keep web component in private_subnet also it will work. Web frontend component is running on port no.80, because we are putting in the nginx

### Now create CDN Cloud front
It is like caching solution from aws, for example ISP providers also have cache servers, if one person downloads a movie, then ISP will keep this downloaded movie in their cache servers, these servers are created at the edge locations, and if other person wants same movie, then he will get that movie from the ISP cache server, here the internet speed or time response will be speed. Similarly we keep our total roboshop content in the CDN (or) Cache server. So now create Distribution in cloud front in aws console, keep origin domain as "web-dev.daws76s.online", keep as HTTPS. Create the samething using terraform code in VS. (or) Cloud front is a caching solution, it has the edge locations all over the world, we can keep origins as s3 buckets,aws load balancers, so content will be cached in the edge locations. We can save the cost and latency also instead of traffic going to the origin, we can get from the cache, we can also reduce the traffic.

### Points to remember
- AWS will charges for data transfer also, like how much data you transferred
