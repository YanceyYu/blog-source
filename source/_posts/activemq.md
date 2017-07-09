---
title: Spring Boot中集成ActiveMq
date: 2017-07-06 17:41:32
categories: java
tags: spring boot
---
## 添加maven依赖
```
<dependency>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

## 在application.properties中增加如下配置
```
# activemq
# 指定ActiveMQ broker的URL
spring.activemq.broker-url=tcp://localhost:61616
# 指定broker的用户
spring.activemq.user=admin
# 指定broker的密码
spring.activemq.password=admin
# 是否是内存模式，默认为true
spring.activemq.in-memory=true
# 是否创建PooledConnectionFactory，而非ConnectionFactory，默认false
spring.activemq.pool.enabled=false
```
<!-- more -->
## 定义消息队列QUEUE
```
package com.activemq.queue;
import javax.jms.Queue;
import org.apache.activemq.command.ActiveMQQueue;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jms.annotation.EnableJms;

@Configuration
@EnableJms
public class QueueConfig {
    @Bean
    public Queue sendMsgQueue() {
        return new ActiveMQQueue("send-sms-queue");
    }
    
    @Bean
    public Queue counterTradeQueue() {  
        return new ActiveMQQueue("counter-trade-queue");  
    }
}
```

## 消息生产者
```
package com.hgxh.trade.service.impl;

import java.util.Map;

import javax.jms.Queue;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jms.core.JmsMessagingTemplate;
import org.springframework.stereotype.Service;

import com.hgxh.trade.service.AcitveMqService;


@Component
public class AcitveMqServiceImpl implements AcitveMqService {
    
    private static Logger logger = LoggerFactory.getLogger(AcitveMqServiceImpl.class);
    
    @Autowired  
    private JmsMessagingTemplate jmsMessagingTemplate;   
    @Autowired  
    private Queue sendMsgQueue;
    @Autowired  
    private Queue counterTradeQueue;

    @Override
    public void sendMsgQueue(String mobile,String content) {
        final String contentMsg = mobile+"|" + content+"|N";
        try {
            jmsMessagingTemplate.convertAndSend(sendMsgQueue, contentMsg); 
        } catch (Exception e) {
            logger.error("send msgQueue fail ", e);
        }
    }

    @Override
    public void sendCounterTradeQueue(Map<String, String> msg) {
        try {
            jmsMessagingTemplate.convertAndSend(counterTradeQueue, msg); 
        } catch (Exception e) {
            logger.error("send counterTradeQueue fail ", e);
        }
    }

}
```

## 消息消费者
```
package com.hgxh.trade.activemq.listener;

import java.util.Map;

import org.apache.commons.lang3.exception.ExceptionUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jms.annotation.JmsListener;
import org.springframework.stereotype.Component;

@Component
public class activeMqListener {

    private static final Logger logger = LoggerFactory.getLogger(LoanListener.class);

 
    @JmsListener(destination = "send-sms-queue")
    public void receiveMsgQueue(String msg) {
        logger.info("activemp send-sms-queue receive msg: " + msg);
        try {
            //执行其他操作
        } catch (Exception e) {
            logger.error("activemp send-sms-queue execute error,Exception : {}", ExceptionUtils.getStackTrace(e));
        }
    }
    
    @JmsListener(destination = "counter-trade-queue")
    public void receiveCounterTradeQueue(Map<String,String> map) {
        logger.info("activemp counter-trade-queue receive map: " + map);
        try {
            //执行其他操作
        } catch (Exception e) {
            logger.error("activemp counter-trade-queue execute error,Exception : {}", ExceptionUtils.getStackTrace(e));
        }
    }


}

```