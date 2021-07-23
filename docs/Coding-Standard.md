## Coding Standard

编程风格有很多，各公司也有各规则。当项目人数变多，代码庞大时，一个好的编程规则起到事半功倍的作用。下面是FreeRTOS的代码风格。

### Style Guide of C

这里对主要内容总结，也可以访问官方网站 [Coding Standard and Style Guide](https://www.freertos.org/FreeRTOS-Coding-Standard-and-Style-Guide.html).

#### 变量命名

不同的变量类型在变量前面加入如下前缀：

    * float --> f
    * double --> d
    * uint8_t(unsigned char) / int8_t(char) --> uc / c
    * uint16_t(unsigned short) / int16_t(short) --> us / s
    * uint32_t(unsigned long) / int32_t(long) --> ul / l
    * 非 stdint.h 定义的有 / 无符号类型变量 --> ux / x
    * 枚举前面使用e
    * 指针前面使用p，例如：uint8_t *pucDemo
    * char 类型的变量只能使用于ASCII字符，前缀c
    * char * 类型的变量只使用于ASCII字符串，前缀pc

#### 函数命名

    * 文件内部函数(static)以prv为前缀 
    * API函数以其返回值类型为前缀， 无返回值前缀为v
    * 函数的名字以其所在的文件名开头。如vTaskDelete函数在Task.c文件中定义

#### 宏命名

    * 宏名以所在的文件的文件名的一部分作为前缀（开头），并且用小写。 比如: configUSE_PREEMPTION 在文件 FreeRTOSConifg.h 中 
    * 除了前缀，其余部分用大写，下划线来分隔单词

#### 数据类型

只使用 stdint.h 定义的数据类型，但是下面两个条件除外：

    * char 只能保存ASCII字符
    * char * 只能保持ASCII字符串 

不能直接使用 int，要使用 short 和 long.

#### 编程风格
 
    * 缩进：缩进使用制表符，一个制表符等于4个空格
    * 注释：注释单行不超过80列，特殊情况除外。不使用C++风格的双斜线（//）注释
    * 布局：FreeRTOS的源代码被设计成尽可能的易于查看和阅读
   
下面的代码片中，第一部分展示文件布局，第二部分展示C代码设计格式：

    /* 首先在这里包含库文件... */    
    #include <stdlib.h>    
        
    /* ...然后是FreeRTOS的头文件... */    
    #include "FreeRTOS.h"    
        
    /* ...紧接着包含其它头文件. */    
    #include "HardwareSpecifics.h"    
        
    /* 随后是#defines, 在合理的位置添加括号. */    
    #define A_DEFINITION    ( 1 )    
        
    /*  
    * 随后是Static (文件内部的)函数原型,   
    * 如果注释有多行，参照本条注释风格---每一行都以’*’起始.  
    */    
    static void prvAFunction( uint32_t ulParameter );    
        
    /* 文件作用域变量（本文件内部使用）紧随其后，要在函数体定义之前. */    
    static BaseType_t xMyVariable.    
        
    /* 每一个函数的结束都有一行破折号，破折号与下面的第一个函数之间留一行空白。*/    
        
    /*-----------------------------------------------------------*/    
        
    void vAFunction( void )    
    {    
        /* 函数体在此定义，注意要用大括号括住 */    
    }    
    /*-----------------------------------------------------------*/    
        
    static UBaseType_t prvNextFunction( void )    
    {    
        /* 函数体在此定义. */    
    }    
    /*-----------------------------------------------------------*/  
    
    /* 
    * 函数名字总是占一行，包括返回类型。 左括号之前没有空格左括号之后有一个空格， 
    * 每个参数后面有一个空格参数的命名应该具有一定的描述性.  
    */    
    void vAnExampleFunction( long lParameter1, unsigned short usParameter2 )   
    {    
    /* 变量声明没有缩进. */    
    uint8_t ucByte;    
        
        /* 代码要对齐.  大括号占独自一行. */    
        for( ucByte = 0U; ucByte < fileBUFFER_LENGTH; ucByte++ )    
        {    
            /* 这里再次缩进. */    
        }    
    }    
        
    /*  
    * for、while、do、if结构具有相似的模式。这些关键字和左括号之间没有空格。 
    * 左括号之后有一个空格，右括号前面也有一个空格，每个分号后面有一个空格。 
    * 每个运算符的前后各一个空格。使用圆括号明确运算符的优先级。不允许有0 
    * 以外的数字（魔鬼数）出现，必要时将这些数字换成能表示出数字含义的常量或 
    * 宏定义。 
    */    
    for( ucByte = 0U; ucByte < fileBUFFER_LENGTH; ucByte++ )    
    {    
    }    
    
    while( ucByte < fileBUFFER_LENGTH )    
    {    
    }    
        
    /*  
    * 由于运算符优先级的复杂性，我们不能相信自己对运算符优先级时刻保持警惕 
    * 并能正确的使用，因此对于多个表达式运算时，使用括号明确优先级顺序  
    */    
    if( ( ucByte < fileBUFFER_LENGTH ) && ( ucByte != 0U ) )    
    {    
        ulResult = ( ( ulValue1 + ulValue2 ) - ulValue3 ) * ulValue4;    
    }    
    
    /* 条件表达式也要像其它代码那样对齐。 */    
    #if( configUSE_TRACE_FACILITY == 1 )    
    {    
        /* 向TCB增加一个用于跟踪的计数器. */    
        pxNewTCB->uxTCBNumber = uxTaskNumber;    
    }    
    #endif    
        
    /*方括号前后各留一个空格*/    
    ucBuffer[ 0 ] = 0U;    
    ucBuffer[ fileBUFFER_LENGTH - 1U ] = 0U; 
