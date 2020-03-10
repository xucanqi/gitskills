### the first program  
```c
#include "reg52.h"  

sbit led =P2^0; //P20口应该写为P2^O 且P为大写  
void main（） 
{
    while（1）
    {
        led=0；//led输出0（低电平）才能点亮
            //led阳极接正极才能正常工作
    }
}
```

