```c
#include <stdio.h>
#include <unistd.h>

int main()
{
  long i;

  sleep(10);
  for (i=0;i<=40000;i++);

  printf("Value of i is: %d",i);
  return 0;
}
```

![My Code Output](images/backgroundprocess.png)
