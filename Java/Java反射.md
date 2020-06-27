现有一个接口`UserService` 和实现类`UserServiceImpl` 要对实现类进行增强

**UserService**

```java
public interface UserService {

    void getUser();

    default void getUser1() {
        System.out.println("default getUser1");
    }
}
```
**UserServiceImpl**

```java
public class UserServiceImpl implements UserService {
    @Override
    public void getUser() {
        System.out.println("原生userService");
    }
}
```

## 静态代理

1. 定义一个类UserServiceStaticProxy 实现UserService 接口
2. UserServiceStaticProxy 中定义一个成员变量为`UserService`
3. 实现方法  前后增强  中间调用`UserServiceImpl`的方法

```java
public class UserServiceStaticProxy implements UserService {
    private UserService userService;

    public UserServiceStaticProxy(UserService userService) {
        this.userService = userService;
    }

    @Override
    public void getUser() {
        System.out.println("代理userService 执行前");
        userService.getUser();
        System.out.println("代理userService 执行后");
    }
}
```

```java
//静态代理
UserService userService = new UserServiceImpl();
UserService userServiceProxy = new UserServiceStaticProxy(userService);
userServiceProxy.getUser();
```

## 动态代理- JDK代理

**原理 反射生成新的类 实现接口。  所以原类必须实现接口**

核心步骤

1. 写过handler继承InvocationHandler
2. 实现invoke方法  前后增强
3. Proxy.newInstance 生成代理类 参数 classLoader 原类接口 handler

```java
public class UserServiceJdkProxyHandler implements InvocationHandler {
    private Object object;

    public UserServiceJdkProxyHandler(Object object) {
        this.object = object;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("jdk代理执行前");
        Object invoke = method.invoke(object, args);
        System.out.println("jdk代理执行后");
        return invoke;
    }
}
```

```java
//jdk 代理
UserServiceJdkProxyHandler userServiceJdkProxyHandler = new UserServiceJdkProxyHandler(userService);
UserService jdkProxyUserService = (UserService) Proxy.newProxyInstance(Demo.class.getClassLoader(), userService.getClass().getInterfaces(), userServiceJdkProxyHandler);
jdkProxyUserService.getUser();
```

## 动态代理-CGLIB代理

**原理： 将原类作为父生成子类 要求  原类不能用FInal修饰  底层ASM 字节码技术**

核心步骤：

1. 写过proxy类实现MethodInterceptor
2. 重写intercept方法
3. Enhancer 创建增强类



```java
public class UserServiceCglibProxy implements MethodInterceptor {
    @Override
    public Object intercept(Object o, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        System.out.println("cglib代理执行前");
        Object o1 = methodProxy.invokeSuper(o, objects);
        System.out.println("cglib代理执行后");
        return o1;
    }
}
```

```java
//cglib代理
UserServiceCglibProxy cglibProxy = new UserServiceCglibProxy();
Enhancer enhancer = new Enhancer();
enhancer.setCallback(cglibProxy);
enhancer.setSuperclass(userService.getClass());
UserService cgLibProxyUserService = (UserService) enhancer.create();
cgLibProxyUserService.getUser();
```





