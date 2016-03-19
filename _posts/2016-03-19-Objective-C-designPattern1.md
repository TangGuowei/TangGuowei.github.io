---
layout: post
title: "设计模式笔记-1"
date: 2016-03-19 00:00:00
image: '/assets/img/'
description: '简单工厂模式.'
tags:
- 设计模式
- 架构
- iOS
categories:
- 框架
twitter_text: 'Put your twitter description here.'
---

## 简单工厂模式

---

###1. 由来场景:
界面中可能会有多种Button，有的方的，有的带圆角，有的可能还有其他形状的。如果不同按钮的创建逻辑放在客户端，我们修改按钮样式或者增加按钮，就必须修改客户端代码，耦合较高。
- 客户端实际上只需要理解这个是个按钮，不关心它是什么类型的按钮。
- 如果将这些不同按钮的创建逻辑提取出来，给一个单独的工厂类管理，客户端只需要告诉工厂按钮的类型，工厂类就可以创造相应特征的按钮，然后返回按钮给客户端使用

###2. 模型结构:
**工厂（Factory）**:负责所有种类的产品创建。根据不同的产品类型创建不同产品，以统一的形式(**Product**)返回给客户端使用

**抽象产品(Product)**:客户端理解的可以是接口或者父类形式，提供给客户端需要知道的产品信息，具体产品需要实现该接口或者继承自改父类。

**具体产品**: 实现抽象产品接口，实际产品可会带上自己的相应业务特性，客户端并不需要知道。

**类图**:
![简单工厂](https://www.processon.com/chart_image/id/56ed6f07e4b07e023d7d9ede.png)

###3. 伪代码:

    //抽象产品
    @interface Product:NSObject
        - (void)use;
    @end

    //具体产品
    @interface ProductA:Product
        - (void)use;
    @end

    @interface ProductA:Product
        - (void)use;
    @end

    //工厂
    @implementation Factory
    + (Product *)productWithType:(Type)type
    {
        if(type == ProductA){
            return [ProductA new];
        }else if(type == ProductB){
            return = [ProductB new];
        }else{
        }
    }
    @end

    客户端

    - (void)configProduct
    {
        Product *product = [Factory productWithType:ProductA];
        [product use];
    }


###4. 模式优点:
- 将构造产品的业务逻辑分离给单独的工厂类管理，客户端只需要使用产品，不需要负责创建
- 使用者，只需知道要抽象产品，和产品类型就可以通过工厂创建不同特征的具体产品。不需要记住不同产品的类名。
- 通过读取配置文件，可以不用带动代码就可以新增和更换产品。增加灵活性

###5. 缺点
- 如果产品过多，工厂类的构造方法复杂度变高，一旦维护者修改出错，可能导致系统不可用
- 不易与扩展，如果新加入产品种类，有可能需要修改工厂代码
- 增加类的数目
