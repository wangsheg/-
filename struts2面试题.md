# 1 Struts2与Struts1的联系与区别 为什么要用Struts2?
  struts1与struts2都是mvc框架的经典实现模式。
  Struts2不是从Struts1升级而来,而是有WebWork改名而来,而WebWork只是Xwork加了很多WEB拦截器而已
  区别：
  1.核心控制器改成了过滤器（过滤器比Servlet的级别要高，因为程序运行时是先进入过滤器再进入Servlet）
  2.struts1要求业务类必须继承Action或dispatchAction，struts2不强制这么做，只需要提供一个pojo类
  3.绑定值到业务类时struts1是通过ActionForm，struts2是通过模型或属性驱动直接绑定到Action属性。
  4.struts1严重依赖于Servlet（因为太过于依赖于api的HttpServletRequest与HttpServletResponse的两个参数），struts2就则脱离了Servlet的API。
  5.管理Action时struts1是单例模式，struts2是每个请求产生一个实例。
  6.在表达式的支持上struts2不仅有jstl，还有功能更加强大的ognl表达式。
  7.struts1的类型转换是单向的（页面到ActionForm），struts2是双向的(页面到Action再到页面回显)
  8.校验，struts1没有针对具体方法的校验，struts2提供了指定某个方法进行效验，还有框架校验。
  9.struts2提供了拦截器，利用拦截器可以在访问Action之前或之后增加如权限拦截等功能。
  10.struts2提供了全局范围，包范围，Action范围的国际化资源文件管理实现。
  11.struts2支持多种视图类型，如：jsp，freemaker，velocity，源代码等。
# 2.Struts2的核心是什么,体现了什么思想?
  Struts2的核心是拦截器,基本上核心功能都是由拦截器完成,拦截器的实现体现了AOP(面向切面编程)思想
# 3 为何继承ActionSupport?
  因为ActionSupport实现了Action接口，提供了国际化，校验功能。ActionSupport实现了国际化功能：因为它提供了一个getText(String key)方法实现国际化,
  该方法从资源文件上获取国际化信息。Action接口提供了五个常量(success,error,login,input,none)。
# 4 Struts2 如何定位action中的方法?
  1 感叹号定位方法（动态方法）。
  2 在xml配置文件中通过配置多个action，使用action的method指定方法。
  3 使用通配符(*)匹配方法。
# 5 模型驱动与属性驱动是什么 模型驱动使用时注意什么问题?
  模型驱动与属性驱动都是用来封装数据的。
  1.模型驱动：在实现类中实现ModelDriven<T>接口使用泛型把属性类封装起来，重写getModel()方法，然后在实现类里创建一个属性类的实例，
  通过这个实例拿到封装进来的值，拿返回值的时候使用工具进行值拷贝。
  2.属性驱动：在实现类里定义属性，生成get与set方法，通过属性来拿值。
  注意：模型驱动使用时注意的是在使用前先把属性类实例化，否则会出现空指针错误，拿返回对象的值需要用拷贝内存因为地址发生改变。
  模型驱动不可以使用局部类型转换器。
# 6.Struts2是怎样进行值封装的？
  struts2的值封装实际上是采用了ognl表达式.
  struts2的拦截器经过模型驱动时会先判断action是否实现了ModelDriven，如果是则拿到模型的实例放在了栈的顶部，
  到属性驱动的时候会从栈里面把栈顶的实例给取出来，从页面传进来的值放在一个map集合当中，通过map集合进行迭代会通过ognl技术把值封装到实例中。
################
