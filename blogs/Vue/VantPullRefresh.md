---
title: 解决 Vant 下拉刷新发送两次请求的问题
date: 2021-11-25
sidebar: 'auto'
categories:
- Vue
tags:
- Vue
- Vant
publish: true
---

### 问题

> 当下拉刷新和上拉加载组合使用时，可能会出现下拉刷洗发送了2次请求的行为。

### 原因

> 究其原因，其实是List组件本身的问题。List 组件的 Load 事件是异步的并且在组件显示的时候会自动触发一次，但是如果请求的内容不足以填满显示区域，List 会继续触发 Load 事件，直到数据足以铺满屏幕，或者数据加载完成。

### 解决

> 可以在 pull-refresh 组件的 刷新事件中先将 List 组件 的 finished 设置为 true，由于 List 组件的特性，在展示的时候会自动触发 Load 事件加载数据。

```
// 下拉刷洗新代码
const onRefresh = () => {
  // 1.清空数据
  indexData.value = {};
  productsData.value = [];
  // 2.页码还原
  page = 1;
  // 3.触底加载状态还原
  state.loading = false;
  // 在这里将 List 的 finished 设置为true
  state.finished = true;
  // 4.重新发送请求
  initIndexData();
  initProductsData();
};
```

> 之后根据请求到的内容再判断 finished 的状态是 false 还是 true

```
const initProductsData = async () => {
  const { data } = await getProductList({
    limit,
    page,
  });
  if (data.status !== 200) {
    return;
  }
  // 数据存储至商品列表
  productsData.value.push(...data.data);
  // 加载状态变更为false
  state.loading = false;
  // 判断是否已经加载完所有产品
  if (data.data.length < limit) {
    state.finished = true;
    return;
  } else {
    state.finished = false;
  }
  // 变更页数，准备下次数据请求
  page += 1;
};
```



在用 Vue3 + Vant3 做项目的时候遇到的小问题，卡了我半小时，哈哈哈哈哈哈哈。

