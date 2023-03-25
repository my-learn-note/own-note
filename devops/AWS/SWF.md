# SWF

## 什么是SWF

**Amazon Simple Workflow Service (Amazon SWF)** 提供了给应用程序异步、分布式处理的流程工具。

SWF可以用在媒体处理、网站应用程序后端、商业流程、数据分析和一系列定义好的任务上。

当用户在电商网站上下单后，即启动了该流程，该流程包含了4个任务（tasks）：

1. SWF验证用户订单信息
2. 如果订单有效，则进行信用卡付款流程
3. 如果付款完毕，则进行人工发货
4. 如果发货完成，则保存订单信息到数据库，并结束流程

在这个流程中，每一个任务都是按顺序执行的，只有当上一个任务成功完成后才能执行下一个任务。

SWF除了支持顺序执行的流程之外，也支持并行处理的流程，即一个任务的完成可以触发多个任务同时执行。

## SWF概念

- SWF发起者（Starter）
  - 可以激活一个工作流的应用程序，可能是电商网站上下单的行为，或者是在手机APP上点击某个按钮
- SWF决策者（ Decider）
  - SWF Decider决定了任务之间的协调，处理的顺序，并发性和任务的逻辑控制
- SWF参与者（Worker）
  - SWF Worker可以在SWF中获取新的任务，处理任务，并且返回结果
- SWF域（Domains）
  - 域包含了工作流的所有组成部分，比如工作流类型和活动类型

SWF决策者和参与者可以是运行在AWS上的EC2实例或者其他计算资源，SWF只是保存不同的任务，把这些任务分配给worker，并且监控

他们的任务处理进展。

## SWF和SQS的区别

- SWF是面向任务的；SQS是面向消息的；
- SWF保证了每一个任务都只执行一次而不会重复；标准的SQS消息可能会被处理多次
- SWF保证了程序内所有任务都正常被处理，并且追踪工作流；而SQS只能在应用程序的层面追踪工作流
- SWF内的任务最长可以保存1年；SQS内的消息最长只能保存14天