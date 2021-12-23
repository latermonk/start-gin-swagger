#   golang gin 框架使用 swaggo



*  swag init
*  go run main.go



---


* main.go

```
/**
 * Created by dongBao on 10/06/2019
 */

package main

import (
	"github.com/gin-gonic/gin"
	ginSwagger "github.com/swaggo/gin-swagger"
	"github.com/swaggo/gin-swagger/swaggerFiles"
	//_ "./docs"
	_ "main/docs"
	"net/http"
)

// @title 测试
// @version 0.0.1
// @description  测试
// @BasePath /api/v1/
func main() {
	r := gin.New()

	// 创建路由组
	v1 := r.Group("/api/v1")

	v1.GET("/record/:userId", record)

	v1.GET("/sayHello/:name", sayHello)

	// 文档界面访问URL
	// http://127.0.0.1:8080/swagger/index.html
	r.GET("/swagger/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))

	r.Run()
}

// @获取指定ID记录
// @Description get record by ID
// @Accept  json
// @Produce json
// @Param   some_id     path    int     true        "userId"
// @Success 200 {string} string	"ok"
// @Router /api/v1/record/{some_id} [get]
func record(c *gin.Context) {
	c.String(http.StatusOK, "ok")
}

// @你好世界
// @Description 你好
// @Accept  json
// @Produce json
// @Param   name     path    string     true        "name"
// @Success 200 {string} string	"name,helloWorld"
// @Router /api/v1/sayHello/{name} [get]
func sayHello(c *gin.Context) {
	name := c.Param("name")
	c.String(http.StatusOK, name+",helloWorld")
}
```
