---
title: Vue.js 生命周期
date: 2021-11-09
sidebar: 'auto'
categories:
- Vue
tags:
- Vue
- 面试
publish: true
---

- Vue.js 生命周期
    - Vue实例的生命周期指的是，实例从创建到运行，再到销毁的过程。
    - Vue.js 生命周期函数，通过设置生命周期函数，可以在生命周期的特定阶段执行功能。
        1. 创建阶段：每个生命周期都只执行一次（特点）
            - beforeCreate( ): 实例初始化之前调用
                
                此时data，methods等，都还未生成，几乎不使用这个生命周期
                
            - created( ): 实例创建后调用
                
                此时data，methods等功能都已经创建完毕，可以在此阶段向服务器请求数据。
                
            - beforeMount( ): 实例挂载前调用
                
                此时页面模板内容还没被添加到DOM中。
                
            - mounted( ): 实例已经挂载完毕
                
                此时使用$el 已经可以访问到值了，可以进行DOM操作。
                
        2. 运行阶段：按需调用（特点）
            - beforeUpdate( ): 数据更新后，视图更新前调用
                
                在这个阶段操作DOM，可以访问到更新前的视图结构。
                
            - updated( ): 视图更新后调用
                
                此时数据和视图都已经更新完毕。
                
        3. 销毁阶段：按需调用（特点）
            - beforeDestory( ): 实例销毁前调用
                
                在这个阶段所有功能都还能正常使用。
                
            - destoryed( ): 实例销毁后调用
                
                此时实例的所有功能都被销毁。