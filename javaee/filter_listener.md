# Chapter 7 Filter & Listener

1. `Filter`
    - 过滤器 实现了这个接口的类
    - `javax.servlet.Filter` Interface   接口
    - 注解式配置
    - 统一编码过滤器

      ```java
      package filter;

      import javax.servlet.*;
      import javax.servlet.annotation.WebFilter;
      import javax.servlet.annotation.WebInitParam;
      import java.io.IOException;

      /**
       * Created by non-perfectionist
       * 8:56 2016/5/6.
       */
      @WebFilter(
              urlPatterns = "/*",
              initParams = @WebInitParam(name = "encoding", value = "UTF-8"))
      public class EncodingFilter implements Filter {

          private String encoding;

          @Override
          public void init(FilterConfig filterConfig) throws ServletException {
              encoding = filterConfig.getInitParameter("encoding");
          }

          @Override
          public void doFilter(ServletRequest request, ServletResponse response, 
                  FilterChain chain)
                  throws IOException, ServletException {

              request.setCharacterEncoding(encoding);
              response.setCharacterEncoding(encoding);
        //chain jQuery方法的链式调用
              chain.doFilter(request, response);
          }

          @Override
          public void destroy() {}
      }
      ```
     
2. `Listener`
    - 监听器 9个接口
    - `request` 相关监听器接口
        1. ServletRequestListener
        2. ServletRequestAttributeListener
    - `session` 相关监听器接口
        1. HttpSessionListener 重要
        2. HttpSessionActivationListener
        3. HttpSessionAttributeListener 重要
        4. HttpSessionBindingListener
        5. HttpSessionIdListener
    - `application` 相关监听器接口
        1. ServletContextListener
        2. ServletContextAttributeListener
    - 注解式配置
        
        ```java
        @WebListener
        ```