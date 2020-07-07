#Mybatis

###一级缓存

　　一级缓存的生命周期有多长？

　　a、MyBatis在开启一个数据库会话时，会 创建一个新的SqlSession对象，SqlSession对象中会有一个新的Executor对象。Executor对象中持有一个新的PerpetualCache对象；当会话结束时，SqlSession对象及其内部的Executor对象还有PerpetualCache对象也一并释放掉。

　　b、如果SqlSession调用了close()方法，会释放掉一级缓存PerpetualCache对象，一级缓存将不可用。

　　c、如果SqlSession调用了clearCache()，会清空PerpetualCache对象中的数据，但是该对象仍可使用。

　　d、SqlSession中执行了任何一个update操作(update()、delete()、insert()) ，都会清空PerpetualCache对象的数据，但是该对象可以继续使用。
  
  ###二级缓存实现
  
    1.Bean继承serialzable接口，实现序列化(如果存储在内存中的话，实测不序列化也可以的。)
    
    2.在映射文件中开启二级缓存
    
      <cache eviction="LRU" flushInterval="100000" readOnly="true" size="1024"/>
      
      <!--可以通过设置useCache来规定这个sql是否开启缓存，ture是开启，false是关闭-->
      
      <select id="selectAllStudents" resultMap="studentMap" useCache="true">
      
          SELECT id, name, age FROM student
          
      </select>
      
     3.在 mybatis-config.xml中开启二级缓存
      <configuration>
        <settings>
            <!--这个配置使全局的映射器(二级缓存)启用或禁用缓存-->
            <setting name="cacheEnabled" value="true" />
          .....
        </settings>
       ....
      </configuration>
