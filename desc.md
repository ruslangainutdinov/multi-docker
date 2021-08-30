
#### Elastic Container Service also refers as ECS
- Task defitions(1 json Dodckerrun.aws.json file with multiple containers inside it, up to 10)
- Container Definitions - inside Task Definition

'{
    "AWSEBDockerrunVersion": "2", - Vesion of syntax
    "containerDefinitions": [
        {
            "name":"client",                                    - name of container
            "image":"ruslangainutdinov7/multi-client",          - base image ref
            "hostname":"client",                                - hostname, as name in docker-compose file; can be used to refer to
            "essential": false                                  - if essential is **true** all other container will shotdown ,
                                                                if this container is down, each file must have 1 essential container?
            "portMappings" : [                                  
                {                                               - port mapping just like docker-compose port mapping
                    "hostPort": 80,                             
                    "containerPort": "80"
                }
            ],
            "links":["client", "server"],                       - creating ***UNIDIRECTIONAL*** networkbetween nginx and client + server; use name of the container
            "memory": 128                                       - RAM to allocate in MB
        }                                                         
    ]
'}

##### The Platform that we choose when creating application in Elastic Beanstalk defines the configuration that is used and the files that are used for this application to be configuried

##### Using Dockerrun.aws.json is used in 'Multi-container Docker', is it considered as obsolete?

##### check new version which uses docker-compose file instead of Dockerrun.aws.json, true?

As a standalone db, we use *AWS Relational Database Service* or **RDS**

For caching we use *AWS Elasti Cache*

Separation of these containers is essential, cause we don't want to reaload db or cache every time we deploy new code

### AWS Elastic Cache
- automcatically creates and maintains **Redis** instances for you
- easy to scale
- built in logging + maintenance
- probably better security than we can do
- completely seprate from other containers so mb easy to migrate in future

### IMPORTANT fo dev! NODE type should be configured to cheapest option

### AWS Relational Database Service
- automcatically creates and maintains **Redis** instances for you
- easy to scale
- built in logging + maintenance
- probably better security than we can do
- **automated backups and rollbacks**
- completely seprate from other containers so mb easy to migrate in future
                            
In each 'Region' of me AWS account I have One default 'Virtual Private Cloud'

### We can check it in 'VPC dashboard'

Security Group (firewall rules)
- auromatically created when we first create out environment for out Elastic Beanstalk Container
- able to configure Security Groups via *Inbound* or *outbound* rules

What we going to do is to create new Security Group and attach our containers(Elastic Beanstalk, RDS and Elastic Cache) to this new group, need to specify inboudn/outbound rules

###### 0.0.0.0 - all internet or any address(entire web)

### IAM Identity and Access Management
- Add new user to have access to deploy