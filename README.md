# Zone_Code_Mongo_Save

保存的结构:
{
    "id": (12个数字组成的id),
    "name": (地区名字),
    "level": (level为2-5之间的一个整数),
    "pid": (上一个level的id,level为1时,该值位"0"),
}
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