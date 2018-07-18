# Zone_Code_Mongo_Save

保存的结构:
{
    "id": (12个数字组成的id),
    "name": (地区名字),
    "level": (这里是最高层,level为1),
    "subs": [],
}
其中,subs是一个数组,其中每一个元素都是一个对象,其结构如下:
{
    "id": (12个数字组成的id),
    "pid": (上一个level的id),
    "name": (地区名字),
    "level": (level为2-5之间的一个整数),
    "subs": [],
}
即使在第五层(level=5),也有一个subs的成员,但是其值为一个空列表(即[])

对于level,其取值含义如下:
    1: province
    2: city
    3: county
    4: town
    5: village

经查看,我发现并不是所有省市都有5层,比如:
    广东省 -> 东莞市 -> 东城街道办事处 -> 岗贝社区居民委员会
一共只有四层,缺少county层,所以其level为:
    1 -> 2 -> 4 -> 5

同时我还发现,大多数id都是按照这样的规则定的:
    province(2位),city(2位),county(2位),town(3位),village(3位),
但是不知道是不是我看错了,好像也看到过这样的:
    province(2位),city(2位),county(3位),town(2位),village(3位),
对于缺少的某一层,用0来填充,固定每个id都是12位

名叫"error"的那个Collection,你不用去理他...那个表里面存的是遇到乱码的地方,
乱码一共有2处,我这里说一下:
1. http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2017/42/06/84/420684103.html,
这边本来是"高社区居委会",我查了一下,叫"高康社区居委会".
2. http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2017/51/06/81/510681114.html,
这边本来是"青村村民委员会",我查了一下,叫"青村村民委员会"(没看到有叫"青X村"的).