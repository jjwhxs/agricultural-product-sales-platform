### 系统介绍

基于SpringBoot和Vue实现的农产品销售平台采用前后端分离的架构方式， 系统设计了四种角色，分别是用户、商家、管理员以及超级管理员，每种角色拥有不同的菜单权限，用户可以在系统中进行注册、登录、首页、全部商 品、购物车、我的订单、农业资讯、搜索、个人中心、我的收藏等功能模块的操作，商家可以在系统中进行登录、数据概览、个人中心、商品管理、交易管理、库存管理等功能模块的操作，管理员可以在系统中进行登录、数据 概览、个人中心、商品管理、交易管理、系统管理、库存管理、资讯管理等功能模块的操作，超级管理员可以在系统中进行登录、数据概览、个人中心、商品管理、交易管理、系统管理、开发配置、库存管理、资讯管理等功能模块的操作。

### 技术选型

开发工具：idea2022.3+webstorm2021.1

运行环境：jdk17+maven3.6.3+mysql8.0+nodejs18.16.0

服务端技术：springboot+mybatis-plus+jwt+fastjson+spring-security

前端技术：html+css+vue+axios+element-ui+echarts

### 成果展示

系统登录/注册
<img width="1895" height="1029" alt="系统登录注册" src="https://github.com/user-attachments/assets/17ac7649-0ad7-45b2-9b79-e00c17ab72d1" />

用户->首页
<img width="1910" height="3336" alt="用户-首页" src="https://github.com/user-attachments/assets/7811cd07-e1d7-442b-8794-b2bb132a4725" />

用户->全部商品
<img width="1910" height="2757" alt="前台-全部商品" src="https://github.com/user-attachments/assets/4d888f4a-21c9-44ac-a4fa-7d52eb8d36c6" />

用户->购物车
<img width="1910" height="1192" alt="前台-购物车" src="https://github.com/user-attachments/assets/d4e87265-5320-47fd-a014-4a31d8319e63" />

用户->我的订单
<img width="1910" height="2916" alt="前台-我的订单" src="https://github.com/user-attachments/assets/dbe4212e-8a42-4bb7-9dff-c95105540cf3" />

用户->农业资讯
<img width="1910" height="1681" alt="前台-农业咨询" src="https://github.com/user-attachments/assets/c52b1eba-91df-4f05-bb4c-39162aca9205" />

用户->收货地址
<img width="1910" height="1152" alt="前台-收货地址" src="https://github.com/user-attachments/assets/9127da38-7ef8-44f2-9695-97dafef77b8d" />

商家->商品管理
<img width="1900" height="1021" alt="商家-商品管理" src="https://github.com/user-attachments/assets/c4a7ae18-eeec-492c-836b-88b2d2b761be" />

商家->入库管理
<img width="1901" height="1025" alt="商家-入库管理" src="https://github.com/user-attachments/assets/6fb533c2-494a-48ca-adb3-7ebe642ecc95" />

商家->出库管理
<img width="1900" height="1021" alt="商家-出库管理" src="https://github.com/user-attachments/assets/0afc7c26-064b-477c-8dcb-351f8f7c5961" />

超级管理员->数据概览
<img width="1910" height="2012" alt="超级管理员-数据概览" src="https://github.com/user-attachments/assets/647f08de-5da5-4d46-8520-a1c6908e53ad" />

超级管理员->商品分类
<img width="1900" height="1021" alt="超级管理员-商品分类" src="https://github.com/user-attachments/assets/e912c1fb-5976-43ec-a3bc-8ee0d6f43815" />

超级管理员->订单列表
<img width="1900" height="890" alt="超级管理员-订单列表" src="https://github.com/user-attachments/assets/e6d65eb6-6ead-410a-afd7-ec7acbb12282" />

超级管理员->商品评价
<img width="1901" height="1023" alt="超级管理员-商品评价" src="https://github.com/user-attachments/assets/76cc4b23-b4da-4a75-81fb-615803e02fc6" />

超级管理员->物流管理
<img width="1900" height="895" alt="超级管理员-物流管理" src="https://github.com/user-attachments/assets/1ac04a60-4efe-430a-a7d4-48d01ca289f7" />

超级管理员->用户管理
<img width="1910" height="1240" alt="超级管理员-用户管理" src="https://github.com/user-attachments/assets/7c3004a8-34fb-4bec-898e-d5928ed2734a" />

超级管理员->资讯管理
<img width="1910" height="1573" alt="超级管理员-咨询管理" src="https://github.com/user-attachments/assets/0971ce68-f2ad-4d1e-8e0e-486f156570ef" />

### 源码展示

@Tag(name = "库存管理接口")

@RestController

@RequestMapping("/stock")

public class StockController {

    @Autowired
    private StockService stockService;

    @Operation(summary = "创建入库记录")
    @PostMapping("/in")
    public Result<?> createStockIn(@RequestBody StockIn stockIn) {
        return stockService.createStockIn(stockIn);
    }

    @Operation(summary = "创建出库记录")
    @PostMapping("/out")
    public Result<?> createStockOut(@RequestBody StockOut stockOut) {
        return stockService.createStockOut(stockOut);
    }

    @Operation(summary = "获取入库记录列表")
    @GetMapping("/in/list")
    public Result<?> getStockInList(
            @RequestParam(required = false) Long productId,
            @RequestParam(required = false) String supplier,
            @RequestParam(required = false) Integer status,
            @RequestParam(required = false) Long operatorId,
            @RequestParam(defaultValue = "1") Integer currentPage,
            @RequestParam(defaultValue = "10") Integer size) {
        return Result.success(stockService.getStockInList(productId, supplier, status, operatorId, currentPage,
               size));
    }

    @Operation(summary = "获取出库记录列表")
    @GetMapping("/out/list")
    public Result<?> getStockOutList(
            @RequestParam(required = false) Long productId,
            @RequestParam(required = false) Integer type,
            @RequestParam(required = false) Integer status,
            @RequestParam(required = false) Long operatorId,
            @RequestParam(required = false) String customerName,
            @RequestParam(required = false) String orderNo,
            @RequestParam(defaultValue = "1") Integer currentPage,
            @RequestParam(defaultValue = "10") Integer size) {
        return Result.success(stockService.getStockOutList(productId, type, status, operatorId, customerName,
               orderNo, currentPage, size));
    }

    @Operation(summary = "作废入库记录")
    @PutMapping("/in/{id}/invalidate")
    public Result<?> invalidateStockIn(@PathVariable Long id) {
        return stockService.invalidateStockIn(id);
    }

    @Operation(summary = "作废出库记录")
    @PutMapping("/out/{id}/invalidate")
    public Result<?> invalidateStockOut(@PathVariable Long id) {
        return stockService.invalidateStockOut(id);
    }

    @Operation(summary = "删除入库记录")
    @DeleteMapping("/in/{id}")
    public Result<?> deleteStockIn(@PathVariable Long id) {
        return stockService.deleteStockIn(id);
    }

    @Operation(summary = "删除出库记录")
    @DeleteMapping("/out/{id}")
    public Result<?> deleteStockOut(@PathVariable Long id) {
        return stockService.deleteStockOut(id);
    }
    
}

### 账号地址及其它说明

1、地址说明

登录页：http://localhost:8080/

2、账号说明

用户：user1/123456

商家：farmer1/123456

管理员：admin/123456

超级管理员：Sadmin/123456

3、目录结构展示

<img width="744" height="180" alt="目录结构" src="https://github.com/user-attachments/assets/eede582e-e4cd-4fa9-8bce-32ddc70e3136" />

4、项目结构展示

<img width="1571" height="824" alt="项目结构" src="https://github.com/user-attachments/assets/05703e99-7cc2-421b-a3ec-1e8f78a6ec3a" />

5、运行步骤

1、创建数据库、导入sql脚本 

2、修改application.properties中的数据库配置文件，启动服务端

3、在前端工程根目录下打开cmd，执行npm install下载依赖

4、下载完毕后启动前端npm run serve，访问端口

### 获取方式(可远程调试)

访问链接：https://mbd.pub/o/bread/mbd-YZWamJltZA==

若资源获取失败，可添加happy35596339(vx)或2061772307(qq)进行交流
