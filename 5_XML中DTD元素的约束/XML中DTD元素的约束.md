# XML  中 DTD 元素的约束

### 定义元素的语法

使用 ELEMENT 声明元素：

       <!ELEMENT 元素名 内容类型或内容>  

例如：

       <!ELEMENTname (#PCDATA)>  

表示 name 元素的内容为文本数据

代码示例：

        <?xml version="1.0" encoding="UTF-8"?>  

        <!DOCTYPE students [  

        <!ELEMENT students (#PCDATA)>  

        ]>  

        <students>
        Cara Sue  
        </students>  

### 元素类型

元素类型可以是 ANY 或 EMPTY

      <!ELEMENTstu ANY>：  

表示 stu 元素的内容可以是任意元素，也可以是文本数据，也可以是文本数据+子元素，反正就是任意。但是要是 DTD 里已经定义过的元素。

 <!ELEMENTstu EMPTY>：

表示 stu 不能有任何内容，即空元素。例如：

           <stu/>  

代码示例：

        <?xml version="1.0" encoding="UTF-8"?>

        <!DOCTYPE students [
        <!ELEMENT students (student+)>
        <!ELEMENT student (name,age)>
        <!ELEMENT name ANY>
        <!ELEMENT age EMPTY>
        ]>

        <students>

            <student>
                <name>Cara Sue</name>
                <age></age>
            </student>

        </students>

### 元素内容

元素内容可以是文本数据，也可以是子元素

      <!ELEMENT stu (#PCDATA)>  

表示 stu 元素内容为文本，例如： <stu>hello</stu>

     <!ELEMENT stu (name)>

表示 stu 元素内容为 name 子元素，例如<stu><name></name><stu>，但要注意，如果<name>元素没有声明，那么就会出错。  
代码示例:

      <?xml version="1.0" encoding="UTF-8"?>

      <!DOCTYPE students [
           <!ELEMENT students (student+)>
           <!ELEMENT student (name,age,gender)>
          <!ELEMENT name (#PCDATA)>
          <!ELEMENT age (#PCDATA)>
          <!ELEMENT gender (#PCDATA)>
      ]>

     <students>
        <student>
          <name>张三</name>
          <age>20</age>
          <gender>男</gender>
        </student>
    </students>  

### 子元素出现次数

可以使用“?”、“\*”、“+”来指定子元素的出现次数
注意修饰的是，符号**前**的一个括号内的内容，如果没有括号，就添一个括号，那是省略的写法！！！

      <!ELEMENTstu (name?)>

表示 stu 元素可以有 0~1 个 name 子元素，即 name 子元素可有可无。

     <!ELEMENTstu(name*)>

表示 stu 元素可以有 0~n 个 name 子元素；

     <!ELEMENTstu(name+)>  

表示 stu 元素可以有 1~n 个 name 子元素。

### 多个子元素

      <!ELEMENT stu (name,age,sex)>  

表示 stu 必须有三个子元素，分别是 name、age、sex，并且子元素出现的顺序也要与声明的顺序一致。

### 枚举子元素

      <!ELEMENT stu (name | age | sex)>  

表示 stu 只有一个子元素，可以是 name、age、sex 中的任意一个。

代码示例：

      <?xml version="1.0" encoding="UTF-8"?>  

      <!DOCTYPE students [  
          <!ELEMENT students (student+)>
          <!ELEMENT student (name|age|gender)>
          <!ELEMENT name (#PCDATA)>
          <!ELEMENT age (#PCDATA)>
          <!ELEMENT gender (#PCDATA)>
      ]>  

      <students>
         <student>
             <name>张三</name>
          </student>
      </students>

### 复合声明1  

     <!ELEMENT stu(name | age | sex)?>  

表示stu元素可以有0~1个(name | age | sex)，而(name | age | sex)表示name、age、sex其中的一个。  

### 复合声明2  

     <!ELEMENT stu (name | age | sex)*>  
    
表示stu元素可以有0~n个(name |age | sex)，而(name | age | sex)表示name、age、sex其中的一个。  

### 复合声明3  

    <!ELEMENT stu(name | age | sex)+>  

表示stu元素可以有1~n个(name | age | sex)，而(name | age | sex)表示name、age、sex其中的一个。
