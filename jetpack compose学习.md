##### Toast

```kotlin
Toast.makeText(this@MainActivity, "你好", Toast.LENGTH_SHORT).show()
```

##### Column

```kotlin
  Column(
   modifier = Modifier.background(Color.Cyan),//设置背景
   horizontalAlignment = Alignment.CenterHorizontally,//水平居中
   verticalArrangement = Arrangement.Center//垂直居中
   )
```

##### Text

```kotlin
                      Text(
                            text = "Hello World",
                            color = Color.Blue,//设置字体颜色
                            fontSize = 40.sp,//更改字号
                            fontStyle = FontStyle.Normal,//设置斜体
                            fontWeight = FontWeight.Bold,//设置加粗
                            textAlign = TextAlign.Center,//文字对齐
                            modifier = Modifier.width(250.dp)//宽
                                .height(60.dp)//高
                                .background(Color.Yellow),
                            style = TextStyle(
                                fontSize = 50.sp,
                                shadow = Shadow(//阴影
                                    color = Color.Red,
                                    offset = offset,
                                    blurRadius = 3f
                                )
                            ),
                            fontFamily = FontFamily.Monospace,//处理字体
                            maxLines = 1,//设置显示行数
                            )
```

##### TextField

```kotlin
                        OutlinedTextField(//
                            value = text,
                            onValueChange = { text = it },
                            label = { Text("Enter text") },
                            maxLines = 1,
                            textStyle = TextStyle(color = Color.Blue, fontWeight = FontWeight.Bold),
                            modifier = Modifier.padding(20.dp),
                            visualTransformation = PasswordVisualTransformation(),//设置密码显示为星号
                            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Text,//设置键盘类型，数字，字母
                                imeAction= ImeAction.Search,//设置回车绑定功能，搜索,前往。。。
                            )//格式设置
                        )
```

##### LazyRow/LazyColumn

```kotlin
LazyColumn {
    // Add a single item
    item {
        Text(text = "First item")
    }

    // Add 5 items
    items(5) { index ->
        Text(text = "Item: $index")
    }

    // Add another single item
    item {
        Text(text = "Last item")
    }
}
```

##### NavHost 导航

```kotlin
    val navController = rememberNavController()

     NavHost(//注：尽量将NavHost放在页面最外层
                            navController = navController,
                            modifier = Modifier,
                            startDestination = "ColumnTest",//设置开始组合体
                        ) {
                            composable(route = "ColumnTest") {
                                ColumnTest()
                            }//配置导航索引
                            composable(route = "TextTest") {
                                TextTest()
                            }//配置导航索引
                        }


   navController.navigateSingleTopTo("ColumnTest")//跳转调用
    //设置导航时跳转到目的地的单个副本
        private fun NavHostController.navigateSingleTopTo(route: String) =
        this.navigate(route) {
            popUpTo(
                this@navigateSingleTopTo.graph.findStartDestination().id
            ) {
                saveState = true
            }
            launchSingleTop = true
            restoreState = true
        }
```

##### compose协程使用

1.在@Composable方法的构造函数中初始化：

```kotlin
coroutineScope: CoroutineScope= rememberCoroutineScope()

coroutineScope.launch{}
```

然后在触发方法里调用

2.直接使用 GlobalScope

```kotlin
GlobalScope.launch { }
```



3.在viewModel中使用协程需要指定Dispatchers,默认Dispatchers在主线程中运行，耗时操作报错

```kotlin
     viewModelScope.launch (Dispatchers.Default){
            val all = db.messageDao().getAll()
            list.addAll(all)
        }
```



##### Room

build.gradle:

```groovy
plugins {
    id 'kotlin-kapt'
}   
   dependencies { // Room components
    implementation "androidx.room:room-ktx:$rootProject.roomVersion"
    kapt "androidx.room:room-compiler:$rootProject.roomVersion"
    androidTestImplementation "androidx.room:room-testing:$rootProject.roomVersion"
    }
```
























