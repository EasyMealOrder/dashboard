## 框架目录设计、逻辑架构与ECB的关系

**目录结构：**

前端：

```
static
  --images
      --favicon.png
src
  --main.js
  --App.vue
  --api
      --unitedInterface.js
  --assets
      --logo.png
  --components
      --Login
          --Login.vue
      --Detail
          --Detail.vue
      --Main
          --index.vue
          --tabs.vue
          --Home
              --Aside.vue
              --DishList.vue
              --Home.vue
              --ImgCarousel.vue
          --Myself
              --MiddleBlock.vue
              --Myself.vue
          --Plate
              --Plate.vue
              --PlateWrapper.vue
      --Order
          --Order.vue
      --PayResult
          --PayResult.vue
  --router
      --index.js
  --store
      --index.js
      --modules
        --allDishes.js
        --cart.js
        --userInfo.js
```

后端：

```
emo
  --emo
     --urls.py #django的url处理模块
     --settings.py #django的配置模块
  --dishes  #提供菜色和分类相关信息
    --views.py  #提供视图，通过django restful framework提供json信息
    --serializers.py  # 规定了如何让model序列化
    --models.py # 定义了数据模型，通过与模型的交互，完全避免了直接的数据库操作
  --order #提供订单相关的操作，包括订单信息获取，提交订单，取消订单等，内部结构同dishes
  --frontpage #提供扫描获得的桌号的验证服务
  --login #厨师端登陆的方法
  --wslogin #用户登陆，同时模拟了微信验证的体系
  --statistic #一些杂项信息，比如用户反馈等
```

**逻辑架构：**

表示层：分为点餐端界面和厨师端界面

业务层：服务器充当业务层的功能

持久化层：使用MySQL作持久化层

**与ECB关系**：

Entity：代表系统数据，包括菜品，订单等。在后端顶层目录中可以看到。

Boundary：与用户的接口，如：界面、网关、代理等，包括点餐段和厨师端与用户交互的各个界面，体现在前端component目录下。同时后端还使用了nginx反向代理。

Controller：在 Boundary 和 Entity 中衔接的媒介，编排来自 Boundary 的命令的执行。体现在后端框架的emo目录中。

