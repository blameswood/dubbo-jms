dubbo-jms
=========

### ����  
  ����JMS��requestor��ʵ����һ��rpcЭ��<br />  
  ������JMS Server�޹�<br />  
  ʹ��ʱ��Ҫ�ṩһ��jms�ͻ������ӵ����ã��μ�example��<br />  
  <br />  
  1. Consumer ==> JMS Server ==> Provider   Request
  2. Consumer <== JMS Server <== Provider   Reply

  
### �����ṩ��������
    <import resource="jms.xml"/>
    <dubbo:application name="dubbo-demo-provider"/>
    <dubbo:registry address="multicast://224.5.6.7:1234"/>
    <dubbo:protocol name="jms" p:queue="#queue" p:queueConnectionFactory="#queueConnectionFactory" id="jms"/> <!-- jms protocol -->
    <bean id="demoService" class="com.alibaba.dubbo.examples.rpc.jms.DemoServiceImpl"/>
    <dubbo:service ref="demoService" interface="com.alibaba.dubbo.examples.rpc.jms.DemoService" protocol="jms"/>

### ��������������
    <import resource="jms.xml"/>
    <dubbo:application name="dubbo-demo-consumer"/>
    <dubbo:registry address="multicast://224.5.6.7:1234"/>
    <dubbo:protocol name="jms" p:queue="#queue" p:queueConnectionFactory="#queueConnectionFactory"/>
    <dubbo:reference timeout="2000" interface="com.alibaba.dubbo.examples.rpc.jms.DemoService" id="demoService"/>
  
### jms�ͻ�����������
    <bean class="org.apache.activemq.ActiveMQConnectionFactory" id="queueConnectionFactory">
    	    <property name="brokerURL"><value>tcp://localhost:61616</value></property>
    </bean>
    <bean class="org.apache.activemq.command.ActiveMQQueue" id="queue" autowire="constructor">
	    <constructor-arg value="DUBBO"/>
    </bean>