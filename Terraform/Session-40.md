### We have "Behaviours" options in cloud front
- We need to create behaviours like if "/images/* ---> Then apply cache policy.
- If "/media/* ---> Then apply cache policy.
- If default then get the content from ---> "web-dev.daws76s.online"
- Total content is coming from CDN, only images are caching and remaining content from the dynamic 
- Depends upon the project we can create cache policies.
- We can disable the cache policy to the dynamic content and enable to the static content.

### We have other option also "Ordered cache behaviour"
Go through the code in VS.

### We also have "Invalidation" options in cloud front
For example you are going for deployment, because you changed some content, then you need to remove cache from all edge locations, so that cloud front will get latest content again and it will cache again new content, for that only we need to create "Invalidations" on whichever path you want. So that Invalidation will delete this static content which are present in the given paths from all edge locations. So if anybody searches then fresh content will be saved in cache. It is better to create Invalidation after every deployment. Using jenkins only we can create Invalidation.

### How the traffic will go 
- CDN URL will Hit first ---> https://web-cdn.daws76s.online
- It will go to the Behaviour and checks wether we have given any behaviours or not ? Nothing but behaviours
  will be evaluated.
- Then CDN will call api-catalouge, since it is dynamic content this URL will go "web-alb"
- web-dev.daws76s.online ---> will go to /api/catalogue/catagories
- Then we have listeners and rules in "web-alb"
- Listener is 443 and if we get "web-dev" then the request will go the web component.

### We have two types of services 
- VPC based service, where resources are created inside the VPC. (If we apply SG in VPC)
- Non-VPC service, where resources are created outside the VPC. (If we dont apply SG in VPC)

### How the security groups will work here ?
- Web-ALB should accept connections from CDN(Internet) on 443
- From web-ALB to web component
- Web component should accept traffic from port 80 from web-ALB
- From web-ALB to App-ALB
- App-ALB should accept traffic on port 80 from web and vpn
- App-ALB to catalogue
- Catalogue should accept traffic on port 8080 from App-ALB etc. 

### How the overall deployement procces will happen ?
Like for example, if we got a new deployment, say few developers are ready for cart deployment, and few are ready for shipping deployment due to new changes 

### Points to remember
- Cloud front is useful to cache static content, generally not for dynamic content.
- Images from our roboshop project.
- We can disable the cache policy in the default also, so that it will fetech from the origins everytime,
  enable only if you need this.
- We are using cloud-front for our front end website, where the images and static content will cached from the
  cloud-front and remaining content we are getting from the load balancer
- Invalidation is nothing but whenever we go for the new deployment, we delete the old cache content from all
  over the edge locations and again cloud-front will get dynamically and save it.
