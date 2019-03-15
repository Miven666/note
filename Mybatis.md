# Mybatis

[中文官方文档地址](http://www.mybatis.org/mybatis-3/zh/index.html)	[github地址](https://github.com/mybatis)

### SqlSessionFactory

- Mybatis都是以SqlSessionFactory的实例为中心的
- 通过SqlSessionFactoryBuilder获得
- SqlSessionFactoryBuilder通过XML配置或Configuration 的实例

### 延迟加载

| 设置参数               | 描述                                                         | 有效值                 | 默认值                         |
| ---------------------- | ------------------------------------------------------------ | ---------------------- | ------------------------------ |
| lazyLoadingEnabled     | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置fetchType属性来覆盖该项的开关状态。 | true、false            | false                          |
| aggressiveLazyLoading  | 当开启时，任何方法的调用都会加载该对象的所有属性。否则，每个属性会按需加载（参考lazyLoadTriggerMethods). | true、false            | false (true in ≤3.4.1)         |
| lazyLoadTriggerMethods | 指定哪个对象的方法触发一次延迟加载。                         | 用逗号分隔的方法列表。 | equals,clone,hashCode,toString |

- 配置

  ```xml
  <configuration>
      <settings>
          <!-- 开启延迟加载 -->
          <setting name="lazyLoadingEnabled" value="true" />
          <setting name="aggressiveLazyLoading" value="false" />
          <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString" />
        </settings>
  </configuration>
  ```

- Mapper 配置

  ```xml
  <mapper namespace="org.apache.ibatis.submitted.lazy_properties.Mapper">
    <resultMap type="org.apache.ibatis.submitted.lazy_properties.User"
      id="user">
      <id property="id" column="id" />
      <result property="name" column="name" />
    </resultMap>
    <!-- 结果对象 -->
    <resultMap type="org.apache.ibatis.submitted.lazy_properties.User" id="userWithLazyProperties" extends="user">
      <!-- 延迟加载对象lazy1 -->
      <association property="lazy1" column="id" select="getLazy1" fetchType="lazy" />
      <!-- 延迟加载对象lazy2 -->
      <association property="lazy2" column="id" select="getLazy2" fetchType="lazy" />
      <!-- 延迟加载集合lazy3 --> 
      <collection property="lazy3" column="id" select="getLazy3" fetchType="lazy" />
    </resultMap>
    <!-- 执行的查询 -->
    <select id="getUser" resultMap="userWithLazyProperties">
      select * from users where id = #{id}
    </select>
  </mapper>
  ```

- User 实体对象

  ```java
  public class User implements Cloneable {
    private Integer id;
    private String name;
    private User lazy1;
    private User lazy2;
    private List<User> lazy3;
    public int setterCounter;
    
    省略...
   }
  ```

- 执行解析：

  1. 调用getUser查询数据，从查询结果集解析数据到User对象，当数据解析到lazy1，lazy2，lazy3判断需要执行关联查询
  2. lazyLoadingEnabled=true，将创建lazy1，lazy2，lazy3对应的Proxy延迟执行对象lazyLoader，并保存
  3. 当逻辑触发lazyLoadTriggerMethods 对应的方法（equals,clone,hashCode,toString）则执行延迟加载
  4. 如果aggressiveLazyLoading=true，只要触发到对象任何的方法，就会立即加载所有属性的加载

