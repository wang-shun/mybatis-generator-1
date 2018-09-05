# mybtais-generator

#### 项目介绍
mybtais-generator 扩展了mybtai自动生成;
在原有的基础上自动生成 扩展MapperExt.java 和 扩展MapperExt.xml 文件  
并且MapperExt.xml 文件直接继承 原生的Mapper.xml 文件 ;他们为同一个命名空间
所以再MapperExt.xml  中可以直接使用   BaseResultMap

1. 自动生成MapperExt.java文件
2. 自动生成MapperExt.xml 文件
3. 使用Mybatis3 的动态Sql生成
4. 自动生成Repository服务层
5. 自动生成Facade对外接口层
6. 0侵入,纯粹生成代码即可


#### 软件架构
1.只是将Mapper所有类似的方法 用泛型抽象了出来
就不需要每个Mapper都建那些curd的接口

2.自动生成Repository类,主要调用Mapper接口,
以及实现业务

3.Facade 就对外暴露接口层;分布式只提供次模块出去


#### 安装教程

1. xxxx
2. xxxx
3. xxxx

#### 使用说明

1. 可以clone次项目打包使用或者直接下载提供的Jar包使用
2. 将Jar导入到  Dao模板
3. 在Dao模块新建一个生成类


```java

import com.src.common.util.MybatisGeneratorUtil;
import com.src.common.util.PropertiesFileUtil;

import java.util.HashMap;
import java.util.Map;

/**
 * 代码生成类
 * Created by src on 2018/6/25.
 * 放在Dao层下面
 */
public class Generator {


	//Model + ModelExample 存放的路径和包名
	private static String targetProjectDao = "wechat-center/wx-dao";
	private static String modelPack = "com.src.model";

	//Mapper.java + Mapper.xml 存放路径和包名
	private static String mapperPack = "com.src.mapper";
	private static String targetProjectSql = "wechat-center/wx-service/src/main/resources/";
	private static String sqlmapperPack = mapperPack;


	//Repository 存放的路径和包名
	private static String targetRepository = "wechat-center/wx-service";
	private static String repositoryPack = "com.src.repository";

	// 远程接口Facade 的路径和包名
	private static String targetProjectRpcApi = "wechat-center/wx-facade";
	private static String rpcPack = "com.src.rpcapi";


	// 远程接口FacadeImpl 实现类 的路径和包名
	private static String targetProjectRpcService = "wechat-center/wx-service";
	private static String rpcServerPack = "com.src.rpcapi.impl";


	//数据库名
	private static String DATABASE = "activity";
	//需要生成的数据表前缀
	private static String TABLE_PREFIX = "wechat_keyword_";

	//创建人
	private static String author = "src";
	private static String JDBC_DRIVER = PropertiesFileUtil.getInstance("generator").get("generator.jdbc.driver");
	private static String JDBC_URL = PropertiesFileUtil.getInstance("generator").get("generator.jdbc.url");
	private static String JDBC_USERNAME = PropertiesFileUtil.getInstance("generator").get("generator.jdbc.username");
	private static String JDBC_PASSWORD = PropertiesFileUtil.getInstance("generator").get("generator.jdbc.password");


	// 需要insert后返回主键的表配置，key:表名,value:主键名
	private static Map<String, String> LAST_INSERT_ID_TABLES = new HashMap<>();
	static {
		//TODO ..
		LAST_INSERT_ID_TABLES.put("wechat_keyword_activity", "id");
	}

	/**
	 * 自动代码生成
	 * @param args
	 */
	public static void main(String[] args) throws Exception {

		MybatisGeneratorUtil.generator(
				null,
				true,//是否生成Facade 层
				targetProjectDao,targetProjectSql,targetProjectRpcApi,targetProjectRpcService,
				targetRepository,modelPack,mapperPack,repositoryPack,sqlmapperPack,rpcPack,rpcServerPack,
				JDBC_DRIVER,JDBC_URL,JDBC_USERNAME,JDBC_PASSWORD,
				DATABASE,TABLE_PREFIX,LAST_INSERT_ID_TABLES,author
		);


	}

}
```

4. 在Dao的resources新建一个generator.properties文件
```xml
generator.jdbc.driver=com.mysql.jdbc.Driver
generator.jdbc.url=jdbc:mysql://XXXXX:3306/activity
generator.jdbc.username=root
generator.jdbc.password=root
```

5. run main方法 就会自动生成以wechat_keyword_为前缀的所有表的数据

#### 生成效果
![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/111.png)

![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/222.png)

![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/333.png)

![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/444.png)

![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/555.png)

![生成效果](https://gitee.com/shirenchuang/mybtais-generator/raw/master/images/666.png)




#### 参与贡献

1. Fork 本项目
2. 新建 Feat_xxx 分支
3. 提交代码
4. 新建 Pull Request


#### 码云特技

1. 使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2. 码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3. 你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4. [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5. 码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6. 码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)