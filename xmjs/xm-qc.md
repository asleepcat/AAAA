---
layout: xm_page
title: 室内质控系统
---
####开发工具               
- Java       
- Spring，Hibernate,SVN        
- Oracle           
- ExtJs

***         

####开发团队/个人职责/时间/参与度              
核心团队一共五人（需求一人，前端两人，后端两人），本人主要负责质控规则计算，数据提交，知识库等功能后端开发。核心功能开发两个月。后台参与度50%。           

***        

####需求设计                
界面设计采用GUIdesign，数据库采用PowerDesign。            
![login](/img/QC/QC1.png)       

***          

####完成产品           
            
![login](/img/QC/QC2.png)
![login](/img/QC/QC3.png)               
![login](/img/QC/QC4.png)           

***      
    
####部分框架配置      
- 数据库连接池采用阿里的druid              

> 	<!-- 配置数据源 -->
	<bean name="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
		init-method="init" destroy-method="close">
		<property name="driverClassName" value="${jdbc.driverClassName}" />
		<property name="url" value="${jdbc.url}" />
		<property name="username" value="${jdbc.username}" />
		<property name="password" value="${jdbc.password}" />
		<!-- 初始化连接大小 -->
		<property name="initialSize" value="0" />
		<!-- 连接池最大使用连接数量 -->
		<property name="maxActive" value="20" />
		<!-- 连接池最大空闲 -->
		<property name="maxIdle" value="20" />
		<!-- 连接池最小空闲 -->
		<property name="minIdle" value="0" />
		<!-- 获取连接最大等待时间 -->
		<property name="maxWait" value="60000" />
		<!-- <property name="validationQuery" value="${validationQuery}" /> -->
		<property name="testOnBorrow" value="false" />
		<property name="testOnReturn" value="false" />
		<property name="testWhileIdle" value="true" />
		<!-- 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒 -->
		<property name="timeBetweenEvictionRunsMillis" value="60000" />
		<!-- 配置一个连接在池中最小生存的时间，单位是毫秒 -->
		<property name="minEvictableIdleTimeMillis" value="25200000" />
		<!-- 打开removeAbandoned功能 -->
		<property name="removeAbandoned" value="true" />
		<!-- 1800秒，也就是30分钟 -->
		<property name="removeAbandonedTimeout" value="1800" />
		<!-- 关闭abanded连接时输出错误日志 -->
		<property name="logAbandoned" value="true" />
		<!-- 监控数据库 -->
		<property name="filters" value="mergeStat" />
	</bean>

- 自动注入采用注解                 

>           
	<context:component-scan base-package="bme.qc.*.*.service">
		<context:include-filter type="annotation"
			expression="org.springframework.stereotype.Service" />
	</context:component-scan>          
           
