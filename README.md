# TSDK
淘宝系统SDK，用于爬虫


##  淘宝系列爬虫系列SDK
  用于爬虫获取淘宝的数据，更为方便的使用，只需要添加API就可以
  此工具的有点就是简单方便，只要设置了API那么就可以自动生成函数来进行使用

- 现在的缺点就是：

    1.  不够灵活，各个平台的的API没有在统一的类下，全部挂载到了基础类上面，这样使用单一的时候造成了浪费，占用了多的资源但是没有使用到，可能后续会添加各个平台类的实现
    2.  API文件的解析，当各个平台的API收集的越来越多的时候，配置文件也会越来越大，这个使用读取一个大的文件本就费时费力，还容易造成卡死，且json配置文件不支持引入设定，不能够引入其他的配置文件，这个以后可能需要解决
    3.  各个API配置解析的设定，API的解析本就依赖于淘宝平台的API实现，除了开放平台API外其余的都有可能在一段时间后修改或者是消亡，需要时常更新，但是API文件的设定导致更新充分，之后可能会添加配置文件更新设定，用于下载最新的配置文件
    4.  基类对象实现的不够彻底，我以一种取巧的方式来共享各个API的请求对象，但是这个可能不是最好的实现，最开始的想法是实例共享，类似于统一继承类一般，
    但现在就是将实例存放在公共访问区域以实现实例共享访问，期待之后会有更好的方法来实现
    5.  各个函数方法的调试还未完全，现在还没有进行单元测试，且log系统没有运行


##  淘宝开放平台API

  为了解决淘宝开放平台的SDK难用的问题而开发，(不支持Py3且改造后还各种奇怪的问题，一看就不是用Python的人写的)
  通过淘宝API文档解析下载指定的淘宝开放平台文档，然后生成规定格式的json配置文件，最后通过读取配置文件来生成各种不同的API
  只需要在配置文件里面配置开放平台的appkey和密钥，设定需要的环境即可使用API

##  淘宝通用API

  此API是拥有特殊行为的API，例如可以通过访问此链接直接获取到用户的名称或是某些数据，只需要设置url，method请求方式，params参数即可，pamams参数的设定方式同其他的API设定类似，也是列表方式，参数对象也是设置名称和值

##  淘宝H5移动端API

  通过API配置文件的方式生成API函数，可查看api.json配置文件，里面有淘宝H5的配置，配置的解读如下：
    config为公共配置，也就是API请求的域名和路径部分，其余的为API配置
    定义一个API名称，然后以对象的方式写其下的配置信息,
    method是请求的方式，不写默认为get请求
    api是使用的名称，可以通过查看链接参数找到
    v是api链接的版本号，也是里面的一个参数
    其余的参数都可以照着这个方式获取并写入到配置里面，
    data参数使用列表方式来进行定义，第一是为了保持定义的顺序，因为淘宝某些API对传递的顺序有要求，必须和移动端发起的请求顺序一致才行，第二是可以对多项进行精准定义，利用对象的的方式可以设置多个属性，且之后还可以用于扩展
    name为参数的名称，value代表着这个参数的默认值，required代表着这个参数是否是必须的，如果是必须的须由用户提供同名参数才可，未来可能还会添加注释参数，以便以后报错不知道这个参数的作用是什么
  
  淘宝H5对象可以直接实例化，但是需要一个公共配置和一个请求配置，公共配置就是config，而请求配置就是定义的API，然后可以直接当做函数调用传参


##  淘宝APP端API

  此API设定还不完全，不过通过观察请求的方式可以发现加密放在了请求头里面，原本的链接上面没有的加密，不过也不一定，有的请求还是有携带加密参数的，不过之后的API设定应该会简单些，请求头的设置可以动态设置和计算，不过现在加密方式未解决，还未破解出来

